# swipe-decide

[日本語](README.ja.md)

A skill that turns the open decisions piling up in a Claude session into cards you settle by swiping. Right = GO, left = NOPE, up = later, down = details. Claude reads your answers and picks the work back up.

(TODO: add a screenshot or GIF here)

## Why I made it

Claude (Opus 5.5) has gotten smart enough that a lot of what it asks me now is just "yes, go ahead". Settling those with a swipe, and having a bit of fun doing it, makes work and hobby projects feel more enjoyable.

## Install

### As a plugin (one command)

```bash
claude plugin marketplace add masukai/swipe-decide
claude plugin install swipe-decide@swipe-decide-marketplace
```

Run it with `/swipe-decide:swipe-decide`, or just say "let's settle the open decisions".

### As a plain skill (copy a folder)

Copy `skills/swipe-decide/` into `~/.claude/skills/`. Run it with `/swipe-decide`.

## Other tools

The skill is plain `SKILL.md` plus one HTML file, so other tools that read the same format may run it. Only Claude Code has been tested. Outside Claude's app there is no auto-save: the page makes a local `decide.html`, and you paste the copied results into chat.

## How it works

1. Tell Claude "let's decide these quickly" or "sort out the open decisions"
2. You are asked once for a style and a color scheme
3. Claude builds the cards: an artifact when you're on a phone, or a local `decide.html`
4. Swipe through them, then tell Claude "done". If saving isn't possible, use "Copy results" and paste them into chat

## Looks

Three styles, each in light and dark: calm (ink seal on washi paper), pop (retro print), flashy (neon).

## Card types

- Yes/No cards
- Choice cards (pick one of 2 to 4)
- Risk cards (hard to undo; asks once before GO)
- `if_no` (what to do instead when you say NO)

## About this project

This is a hobby project. I update it when I feel like improving it. Requests are welcome as issues, but I can't promise a response time. No need to star it.

## License

MIT
