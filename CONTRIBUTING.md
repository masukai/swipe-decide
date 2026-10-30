# Contributing

Thanks for taking a look. This is a hobby project, so replies may take a while, but contributions are welcome.

## Ideas, bugs, features

Open an issue first for anything bigger than a small fix. Please include what you were trying to decide, which tool you used (Claude Code, the Claude app, something else) and, for visual bugs, a screenshot with the window size.

PRs are welcome. Keep these in mind:

- The skill is two files: `skills/swipe-decide/SKILL.md` and `skills/swipe-decide/assets/template.html`. New files and new features need a good reason.
- The page must keep working as a single HTML file, with no build step and no external libraries.
- `SKILL.md` is English. Card text follows the user's language. `README.md` is the canonical readme and `README.ja.md` stays short.

## Design contributions (very welcome)

The UI lives in `assets/template.html`. Each look is selected by `data-look` (`calm`, `pop`, `flashy`) and each color scheme by `data-scheme` (`light`, `dark`).

Good places to start:

- Polish an existing look: spacing, type, colors, motion.
- Propose a new look as a new `data-look` block of CSS. Please make it work in both light and dark.
- Check small screens. Cards must fit from about 360px tall up, and the result screen must not clip.

Before opening a PR for a visual change, please look at it in all looks and both schemes, at phone width and at a short window, and attach a screenshot or GIF.

## Checks

```bash
claude plugin validate --strict .
```

Then open the page in a browser, swipe through every card type, and confirm the result screen appears.
