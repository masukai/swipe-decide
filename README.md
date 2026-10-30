<div align="center">

# 🃏 swipe-decide

**Decide like a dopamine goblin: swipe through your open decisions.**

A Claude skill that turns the questions piling up in your session into cards.<br>
Swipe right for GO, left for NOPE. Claude picks the work back up with your answers.

**English** · [日本語](README.ja.md)

[![License: MIT](https://img.shields.io/badge/license-MIT-2ea44f.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill%20%26%20plugin-d97757.svg)](#-30-second-start)
[![Check](https://github.com/masukai/swipe-decide/actions/workflows/check.yml/badge.svg)](https://github.com/masukai/swipe-decide/actions/workflows/check.yml)

<img src="docs/demo.gif" alt="Swiping through decision cards: GO, NOPE, Later, with combo and confetti" width="320">

[Quick start](#-30-second-start) · [How to swipe](#-swipe-your-answer) · [Looks](#-looks) · [Contributing](#-contributing)

</div>

## 💭 Why I made it

Claude (Opus 5.5) has gotten smart enough that a lot of what it asks me now is just "yes, go ahead". Typing "yes" over and over felt like a chore, so I turned the questions into cards. Swiping through them takes seconds, and honestly it's kind of addictive. Work and hobby projects got more fun.

## ✨ When it shines

- **Mid-session pile-up.** Claude has five questions for you. Swipe them all in one go instead of answering one by one.
- **After a long unattended run.** Let Claude work overnight or while you're away, then settle everything it was unsure about in one sitting the next morning.
- **Batching your attention.** Let the small calls queue up, then clear them in one burst whenever you have a minute, even from your phone.

## 🚀 30-second start

```bash
claude plugin marketplace add masukai/swipe-decide
claude plugin install swipe-decide@swipe-decide-marketplace
```

Then run `/swipe-decide:swipe-decide`, or simply say "let's decide these quickly."

<details>
<summary>Prefer a plain skill (just copy a folder)?</summary>

Copy `skills/swipe-decide/` into `~/.claude/skills/` and run `/swipe-decide`.

</details>

## 👆 Swipe your answer

| Move | Decision | On a PC |
|:---:|:---:|:---:|
| ➡️ Right | **GO** | `→` |
| ⬅️ Left | **NOPE** | `←` |
| ⬆️ Up | **Later** | `↑` |
| ⬇️ Down | **Details** | `↓` |

On a choice card, tap an option (or press its number) to pick it. Swipe right to take Claude's suggestion.

## 🎨 Looks

Three styles, each in light and dark. Pick one when you start, or let Claude surprise you.

<table>
  <tr>
    <th align="center">Calm</th>
    <th align="center">Pop</th>
    <th align="center">Flashy</th>
  </tr>
  <tr>
    <td align="center"><img src="docs/looks/calm-light.png" alt="Calm, light" width="240"></td>
    <td align="center"><img src="docs/looks/pop-light.png" alt="Pop, light" width="240"></td>
    <td align="center"><img src="docs/looks/flashy-light.png" alt="Flashy, light" width="240"></td>
  </tr>
  <tr>
    <td align="center"><img src="docs/looks/calm-dark.png" alt="Calm, dark" width="240"></td>
    <td align="center"><img src="docs/looks/pop-dark.png" alt="Pop, dark" width="240"></td>
    <td align="center"><img src="docs/looks/flashy-dark.png" alt="Flashy, dark" width="240"></td>
  </tr>
  <tr>
    <td align="center"><sub>ink seal on washi paper</sub></td>
    <td align="center"><sub>cheerful retro print</sub></td>
    <td align="center"><sub>full neon energy</sub></td>
  </tr>
</table>

## 🃏 Card types

- **Yes / No**: make a clean call
- **Choice**: pick one of 2 to 4 options
- **Risk**: one extra check before a hard-to-undo GO
- **Fallback**: choose what happens instead after a NO

## 🔧 How it works

1. Ask Claude to sort out the open decisions.
2. Pick a look and color mode once.
3. Claude turns up to 12 decisions into swipeable cards.
4. Swipe through, say "done," and Claude continues with your choices.

## ❓ Quick notes

**Does this work outside Claude Code?**
The skill is plain `SKILL.md` plus one HTML file, but only Claude Code has been tested.

**Where do my results go?**
In Claude Code and other tools with a shell, Claude starts a tiny local server (127.0.0.1 only, Python standard library) and your results are saved automatically. In the Claude app, an artifact saves them for you. **To swipe on your phone, use the Claude app (the page opens as an artifact); the local server is only reachable from your own computer.** Anywhere else, open the generated `decide-<run>.html`, use **Copy results**, and paste the result back into chat.

## 🤝 Contributing

Feature ideas and bug reports are welcome as issues, and PRs are welcome too. See [CONTRIBUTING.md](CONTRIBUTING.md).

**Designers, this one is for you.** The card UI is a single HTML file, and each look (calm, pop, flashy) is just a block of CSS. A new look, a better one, or a polish pass on an existing one is a great first contribution.

## 🌱 About this project

This is a hobby project, updated when inspiration strikes. Issues are welcome, though I can't promise a response time. Starring is entirely optional.

## 📄 License

[MIT](LICENSE)
