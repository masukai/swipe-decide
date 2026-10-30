# swipe-decide

ドパガキ向け、スワイプで未決事項を片付けるスキル。✨

[English / 詳細はこちら](README.md)

![demo](docs/demo.gif)

## 作った理由

Claude(Opus 5.5)が賢くなって、判断を求められる内容が「はい」と答えるだけのことも増えました。そういうものをスワイプで楽しく決められると、仕事も趣味ももっと面白くなると思って作りました。

## 30秒で始める

```bash
claude plugin marketplace add masukai/swipe-decide
claude plugin install swipe-decide@swipe-decide-marketplace
```

`/swipe-decide:swipe-decide` を実行するか、「未決事項をサクサク決めたい」と話しかければOKです。

右は **GO**、左は **NOPE**、上は **あとで**、下は **詳しく**。PCでは矢印キーでも操作できます。

見た目は calm / pop / flashy の3種類。Yes・No、2〜4択、取り消しにくい判断の確認、NO時の代案に対応します。

詳しい使い方・仕組み・注意点は、正本の [README.md](README.md) を参照してください。Claude Codeでのみテスト済みです。Claudeアプリ外では自動保存されないため、「結果をコピー」してチャットへ貼り付けます。

## このプロジェクトについて

趣味で作っています。issueは歓迎ですが、返事の時期は約束できません。スターはお好みでどうぞ。

## ライセンス

MIT
