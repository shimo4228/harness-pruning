# harness-pruning

**個人用 Claude Code harness から「出ていったもの」の日付つき記録です。決定記録（ADR）を持つ
skill / rule / agent / hook の退役・溶解・縮小を、1 件ずつ理由と根拠つきで並べています。**
ADR を残さずに行った削除は範囲外なので、件数は下限であって総数ではありません。想定読者は、
agent harness に「何を足すか」の話は読んだが「何を外すか」の話はほとんど読んでいない方です。

これは主張ではなく実例（record）です。推奨でもベンチマークでもありません。1 つの harness で
実際に外れたものを、それを認可した決定記録まで辿れる形にして公開しています。外れなかった部分も
含めて、harness が実際にどう縮むのかを見てもらうためのものです。

著者は **Tatsuya Shimomoto (shimo4228)** — <https://github.com/shimo4228> です。
harness 本体は <https://github.com/shimo4228/claude-harness> にあり、ここで引用している ADR は
すべてそちらで公開しています。

---

## 収録内容

| ファイル | 中身 |
|---|---|
| [`LEDGER.md`](LEDGER.md) | 退役イベント 27 件（2026-09-08 時点）。1 行につき、日付 / component / 何を外したか（縮めたか） / 理由 / 不要になったモデル世代（出典が明示している場合のみ） / 認可した ADR。末尾に net change 節。 |
| [`HOWTO.md`](HOWTO.md) | この harness で退役をどう判断しているか。harness 内に既存の 3 文書を出典 path つきで要約したもので、新規に考案した手順はありません。 |

## 都合の悪い部分

harness の全履歴を通して、2026-09-08 時点で、削除された skill ファイルは 68 件、新規作成は
127 件でした。agent 層と rule 層も同じ形ですが比率はやや低く、退役 1 件あたりの追加はおよそ
1.5 件（skill 層は 1.9 件）です。**harness は小さくなっていません。入れ替わっています。**
この事実は隠さず LEDGER の net change 節に書いています。追加を報告せずに
削除だけ報告する台帳は、片側だけを測って傾向と呼んでいることになるからです。

ただし退役には方向性があります。component が抜けるのは、substrate がそれを吸収したときです。
built-in の reviewer が同じ面をカバーすれば reviewer agent は退役します。LSP tool がその場で
導出できるなら、保存された file-level の構造地図は退役します。弱いモデルの判断を補うために
書かれた rule は、その補正が衝突コストに転じた時点で退役します。

## なぜ公開するのか

「engineering の対象はモデルではなく harness である」という主張は、すでに公の場でよく論じられて
います。

- Anthropic, *Harness design for long-running apps*（2026-03-24）—
  <https://www.anthropic.com/engineering/harness-design-long-running-apps>
- Addy Osmani, *Agent harness engineering*（2026-04-19）—
  <https://addyosmani.com/blog/agent-harness-engineering/>
- Philipp Schmid, *The agent harness in 2026*（2026-01-05）—
  <https://www.philschmid.de/agent-harness-2026>

これらは主張です。この repository は、その主張に対する 1 つの公開 instance です。1 つの
harness の退役を、日付と出典をつけて約 6 か月半ぶん並べたものにすぎません。主張が一般化することを
示すものではなく、また網羅調査でもありません（同じ形の公開物が他に何があるかは確認していま
せん）。

## 行の読み方

各行は `~/.claude/docs/adr/` 配下のファイルを引用しており、その実体は `claude-harness` で公開
されています。行を信用する前に ADR 本体を開いてください。とくに次の 2 列は疑ってください。

- **why** — 数ページある ADR を 1 文に圧縮しています。圧縮したのは著者であり、正本は ADR です。
- **model generation** — ADR 自身が世代を名指ししている場合だけ記入し、substrate（built-in・
  tool・公式の既定）に帰している場合は "not model-attributed" と書いています。推論では埋めて
  いません。27 行のうち世代を名指ししているのは 7 行、名指しせず世代交代に帰しているのが 4 行、
  残る 16 行は substrate に帰しています。この内訳自体が 1 つの観測です。これらの component の
  多くは、モデルが賢くなったから不要になったのではなく、製品が機能を持ったから不要になって
  います。

## 限界

- harness 1 つ、著者 1 人、tool 1 つ。比較対象はありません。
- 台帳が拾えるのは ADR がある退役だけです。決定記録を残さずに行った小さな削除は載っていない
  ので、退役件数は下限であって総数ではありません。
- その場で縮めた事例（`skill-creator` が 5,886 行から 96 行になるなど）はファイル数を動かさ
  ないため、net change 表は台帳の行が記述している削減を過小に見せます。

## ライセンス

MIT。[`LICENSE`](LICENSE) を参照してください。
