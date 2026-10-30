# swipe-decide

[English](README.md)

セッション中に溜まった未決事項を、カードにしてスワイプで一気に決めるスキルです。右=GO、左=NOPE、上=あとで、下=詳しく。結果はClaudeがそのまま読んで、作業を再開します。

詳しい説明は英語版(README.md)を正とします。

## 作った理由

Claude(Opus 5.5)が賢くなって、判断を求められる内容が「はい」と答えるだけのことも増えました。そういうものをスワイプで楽しく決められると、仕事も趣味ももっと面白くなると思って作りました。

## 入れ方

```bash
claude plugin marketplace add masukai/swipe-decide
claude plugin install swipe-decide@swipe-decide-marketplace
```

使うときは `/swipe-decide:swipe-decide`。スキル単体で使う場合は `skills/swipe-decide/` を `~/.claude/skills/` にコピーして `/swipe-decide`。

## このプロジェクトについて

趣味で作っています。改善したくなったときに更新します。要望はissueでどうぞ(返事の時期は約束できません)。スターは無理にしなくて大丈夫です。

## ライセンス

MIT
