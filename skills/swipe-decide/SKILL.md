---
name: swipe-decide
description: Use when the user wants to settle many open decisions quickly, says "let's decide these quickly" or "sort out the open decisions," or when 5+ open decisions have piled up in the conversation. Japanese triggers include サクサク決めたい / まとめて決めたい / 未決事項を整理して.
---

# swipe-decide

Turn open decisions into cards, have the user settle them all at once by swiping, and then resume the work according to those results.

## Procedure

1. **Ask about the look (once only)**: Ask about both the style (serious = calm / playful = pop / bold = flashy / surprise me) and color scheme (auto / light / dark) in a single prompt.
   - Do not ask if they have already been specified. If the user chooses "surprise me" or gives no answer, use `pop` and `auto`.
2. **Extract**: Find the items that remain undecided in the conversation. If there are many, take up to 12 in order of impact. Tell the user that the rest will be handled in the "next round."
   - If the previous `decisions.md` contains items marked "on hold," pick those up first (carry them over).
   - Decide low-impact, reversible items yourself instead of turning them into cards.
3. **Break down**: Turn anything that can be decided with Yes/No into a proposition such as "Go with A?" Use a choice card (`options`) when there are 2–4 alternatives the user should compare and choose from. Narrow down sets of 5 or more before presenting them.
4. **Create cards**: Build each card according to the specification below.
   - Set `rec` honestly. Do not make every recommendation `yes`. Use `later` when uncertain.
   - When the alternative action for a NO decision is known, put it in `if_no`.
   - Add `risk: true` to irreversible decisions involving deletion, publication, money, and similar concerns.
   - Write the card text in the language the user is using in the conversation.
5. **Output**: Read `assets/template.html` from the same folder as this SKILL.md, replace only the following two locations, and save the result. Use the code under "Replacement" below.
   - `id="config"`: The answers from step 1 and the run ID `run` (for example, `2026-10-29-2030`; alphanumeric characters and hyphens only). Fix `lang` to the language used for the cards (`ja` / `en`). Use `auto` (to match the device language) only when every card has `i18n`.
   - `id="cards"`: The card JSON.
   - Standard (works with any tool): Write the result to `./decide.html` and open it in a browser. Because results are not saved automatically, ask the user to paste them using "Copy results."
   - Only when the user wants to open it on a phone in the Claude app or use automatic saving: publish it as an artifact and add `{"db":{}}` to `capabilities`.
6. **Wait**: Say only this one line: "When you've decided everything, send 'done.' If it couldn't be saved, follow the on-screen instructions, use 'Copy results,' and paste them here." Even when the page saves the results, Claude is not notified.
7. **Read**: When the user says "done," read the saved data at `results/<run>` (if it was published as an artifact). If it cannot be found or its `status` is not `done`, ask the user to paste the copied results. After reading it, update `status` to `applied`. When the results are provided by pasting, there is no need to read or update saved data.
8. **Resume**: Read the results and proceed according to each `choice` in `decisions`.
   - `yes`: Do it.
   - `no`: Do not do it. **Do not ask for confirmation afterward.** If `if_no` exists, carry out that alternative instead.
   - `pick`: Carry out the option identified by `picked` (the selected option's id).
   - `later`: Ask about these items together again after the other work is complete.
   - Do not interrogate the user about items with `contrarian: true` (opposite to Claude's recommendation). Give a one-line confirmation only when the impact is high.
9. **Record**: When files can be written, append the decisions to `decisions.md`. Keep items that end as `later` marked "on hold" so they can be picked up during the next extraction.

## Card JSON

The character limits and length targets below are for Japanese. For English, use roughly twice as many characters (in particular, `q` <= 80 and `why` <= 120).

| Field | Rule |
|---|---|
| id | Unique string |
| tag | Category name. About 8 characters maximum |
| hue | 0–360 |
| q | A proposition ending in a question such as "Do X?" **40 characters maximum** (the text shrinks above 60 characters and is clipped above 90) |
| why | One sentence. **60 characters maximum** (clipped after 3 lines) |
| detail | Around 150 characters. Include information needed for the decision and points that may cause trouble later. The full text is available under "Details" |
| rec | yes / no / later. For a choice card, the id of the recommended option |
| options | Optional. For choice cards. 2–4 entries shaped as `{id, label, desc?, detail?, i18n?}`. `label` is about 12 characters maximum; `desc` is a short note shown on the card (around 20 characters); `detail` is a longer explanation shown in the detail sheet after a downward swipe (around 100 characters). The user can also decide by tapping an option in the sheet. `why` is not displayed |
| if_no | Optional. What to do instead when the answer is NO. 40 characters maximum |
| risk | Optional. When `true`, adds a red "Caution" mark and asks for confirmation once before GO |
| i18n | Optional. Override tag / q / why / detail / if_no for each language code (`en`). For options, use `options[].i18n` |

Choice card controls: Decide by tapping an option (or pressing its number key). Swipe right = choose Claude's recommendation; left = choose none (`no`); up = later.

The four possible values of `decisions[].choice` in the results are `yes` / `no` / `later` / `pick`.

## Replacement

Because the JSON is inserted into a `<script>`, replace `</` with `<\/`.

```python
import json, re
SKILL_DIR = "..."  # Absolute path to the folder containing this SKILL.md (shown when the skill is loaded)
t = open(SKILL_DIR + "/assets/template.html", encoding="utf-8").read()
cfg = {"look": "pop", "mode": "auto", "lang": "ja", "run": "2026-10-29-2030"}
cards = [...]  # List of card JSON objects
esc = lambda o: json.dumps(o, ensure_ascii=False).replace("</", "<\\/")
t = re.sub(r'(id="config">)[^<]*', lambda m: m.group(1) + esc(cfg), t, count=1)
t = re.sub(r'(id="cards">)[\s\S]*?(</script>)', lambda m: m.group(1) + esc(cards) + m.group(2), t, count=1)
# Add the HTML skeleton only when writing locally (the host adds it when publishing, so it is not needed then)
SKELETON = ('<!doctype html><html><head><meta charset="utf-8">'
            '<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">'
            '<style>html,body{margin:0}</style></head><body>')
open("decide.html", "w", encoding="utf-8").write(SKELETON + t + "</body></html>")
```

Without the skeleton, a phone may show the page scaled down to a desktop width (980px), and text may also be garbled. When publishing as an artifact, save and publish only `t` (do not add the skeleton).

The SAMPLE badge appears on the screen only when `run` is `sample`. Always use a different ID for a real run.

## Rules

- Do not modify the template's CSS or JavaScript. Replace only config and cards.
- Do not add external libraries (it must work as a single file).
- Do not proceed with undecided items until the results can be read.
