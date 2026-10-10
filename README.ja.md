# harness-pruning

**個人用 Claude Code harness から「出ていったもの」の日付つき記録です。アーキテクチャ決定記録（ADR）を持つ skill / rule / agent / hook / plugin / chain の段（タスクごとの agent の並びの 1 段） / 執筆の規約の退役を、1 件ずつ理由と根拠つきで並べています。** ADR を残さずに行った削除は範囲外なので、件数は下限であって総数ではありません。想定読者は、agent harness に「何を足すか」の話は読んだが「何を外すか」の話はほとんど読んでいない方です。

これは記録です。主張でも推奨でもベンチマークでもありません。1 つの harness で実際に外れたものを、それを認可した決定記録まで辿れる形にして公開しています。外れなかった部分も含めて、harness が実際にどう縮むのかを見てもらうためのものです。

著者は **Tatsuya Shimomoto**（[shimo4228](https://github.com/shimo4228)）です。harness 本体は <https://github.com/shimo4228/claude-harness> にあり、ここで引用している ADR はすべてそちらで公開しています。この台帳は harness からの同期ではなく手で編んでいるもので、件数は 2026-09-08 時点です。退役のうち 2 件を扱った記事と関連 repo は [著者のほかの仕事](#著者のほかの仕事) にあります。

---

## 収録内容

| ファイル | 中身 |
|---|---|
| [`LEDGER.md`](LEDGER.md)（英語） | 退役イベント 27 件（2026-09-08 時点）。1 行につき、日付 / 部品 / 何を外したか（縮めたか） / 理由 / 不要になったモデル世代（名指し、名指しせず世代交代に帰す、"not model-attributed" のいずれか） / 認可した ADR。末尾に net change 節。 |
| [`HOWTO.md`](HOWTO.md)（英語） | この harness で退役をどう判断しているか。harness 内に既存の 3 文書を出典 path つきで要約したもので、新規に考案した手順はありません。 |

## 都合の悪い部分

harness の全履歴を通して、2026-09-08 時点で、削除された skill は 68 件、新規作成は 127 件でした（`skills/*/SKILL.md` のパス数）。agent 層と rule 層も同じ形ですが比率は低く、削除 1 件あたりの追加はおよそ 1.5 件（skill 層は 1.9 件）です。**パス数で数えると、harness は小さくなっていません。入れ替わっています。** この事実は隠さず LEDGER の net change 節に書いています。追加を報告せずに削除だけ報告する台帳は、片側だけを測って傾向と呼んでいることになるからです。

ただし 27 行のうち 14 行の退役には方向性があります。部品が抜けるのは、その役目を harness の外にあるものが引き受けたとき、つまり substrate（built-in・tool・公式の既定）か新しいモデル世代が引き受けたときです。built-in の reviewer が同じ範囲を受け持てば reviewer agent は退役します。LSP（language server）tool がその場で導出できるなら、保存されたファイル単位の構造地図は退役します。弱いモデルの判断を補うために書かれた rule は、その補正が衝突コストに転じた時点で退役します。

この方向性がどこまで当てはまるかは、台帳の model generation 列で分かります。27 行のうち世代を名指ししているのは 7 行、名指しせず世代交代に帰しているのが 4 行です。残る 16 行は "not model-attributed" で、そのうち substrate を名指ししているのは 3 行（公式の Workflow / Agent harness、公式 plugin、built-in の `/code-review`）です。ほかの 13 行は harness の内側にある理由を挙げています。重複、使われていなかった部品、スクリプトへ移した機械的な検査、新しく起動した subagent が持たない文脈などです。つまり方向性が当てはまるのは 27 行のうち 14 行で、substrate を名指しする 3 行と、名指しの有無を問わずモデル世代に帰す 11 行です。残る 13 行について、この列は substrate もモデル世代も記していません。

## なぜ公開するのか

「作り込む対象はモデルではなく harness である」という主張は、すでに公の場でよく論じられています。

- Anthropic, *Harness design for long-running apps*（2026-03-24）— <https://www.anthropic.com/engineering/harness-design-long-running-apps>
- Addy Osmani, *Agent harness engineering*（2026-04-19）— <https://addyosmani.com/blog/agent-harness-engineering/>
- Philipp Schmid, *The agent harness in 2026*（2026-01-05）— <https://www.philschmid.de/agent-harness-2026>

この repository は、これらの主張に照らして見るための公開された実例の 1 つです。1 つの harness の退役を、最初の commit（2026-02-26）から 2026-09-08 まで、日付と出典をつけて並べたものにすぎません。主張が一般化することを示すものではなく、また網羅調査でもありません（同じ形の公開物が他に何があるかは確認していません）。

## 行の読み方

各行は `~/.claude/docs/adr/`（著者の手元の harness）配下のファイルを引用しており、その実体は `claude-harness` の [`docs/adr/`](https://github.com/shimo4228/claude-harness/tree/main/docs/adr) で公開されています。行を信用する前に ADR 本体を開いてください。とくに次の 2 列は疑ってください。

- **why** — 数ページある ADR を 1 文に圧縮しています。圧縮したのは著者であり、正本は ADR です。
- **model generation** — ADR 自身が世代を名指ししている場合はその世代を記入し、世代交代に帰しているが名指ししていない場合はそう書き、それ以外は "not model-attributed" と書いて、ADR が substrate に帰している場合はその substrate を添えています。推論では埋めていません。

## 限界

- harness 1 つ、著者 1 人、tool 1 つ。比較対象はありません。
- 台帳が拾えるのは ADR がある退役だけです。決定記録を残さずに行った小さな削除は載っていないので、退役件数は下限であって総数ではありません。
- 部品を残したまま中身を縮めた事例は、net change 表のパス数にほとんど現れません。`skill-creator` は 19 ファイル・5,886 行から、96 行の SKILL.md と 38 行の参照ファイル 1 つになりましたが、`skills/*/SKILL.md` のパスは 1 つも変わっていません。そのため、この表は台帳の行が記述している削減を過小に見せます。

## 著者のほかの仕事

- **[AIレビューを6系統から1系統へ——「指摘ゼロ」で終われないループの切り方](https://zenn.dev/shimo4228/articles/review-chain-damping)**（[English](https://dev.to/shimo4228/i-cut-my-ai-review-chain-from-6-stages-to-1-breaking-the-loop-that-never-hits-zero-findings-1moi)）: 2026-08-27 の行の経緯です。指摘ゼロを待つレビューのループがなぜ終わらないのかと、常設のレビュー 6 系統を 1 系統に縮めた実測が分かります。
- **[3か月で159回commitしたLLM向けアーキテクチャ文書を消した。構造はLSP、理由はADR、図は人間に](https://zenn.dev/shimo4228/articles/codemap-retirement)**（[English](https://dev.to/shimo4228/i-deleted-the-llm-facing-architecture-docs-i-had-committed-159-times-in-3-months-structure-goes-to-1a94)）: 2026-09-05 の行の経緯です。保存していたファイル単位の構造地図を LSP に、その理由を ADR に、図を人間に渡した判断が分かります。
- **[claude-harness](https://github.com/shimo4228/claude-harness)**: 著者が毎日使っている Claude Code harness の公開版です。これらの退役はここから出たものです。
- **[generation-audit](https://github.com/shimo4228/generation-audit)**: 新しい Claude モデルが役割を引き継ぐときに、自分の rule・skill・agent を点検し直す skill です。`HOWTO.md` はその手順を要約しています。
- **[skill-stocktake](https://github.com/shimo4228/skill-stocktake)**: 導入済みの skill を古さ・衝突・重複の観点で棚卸しし、Retire を含む判定を 1 つずつ出します。
- **[human-gate](https://github.com/shimo4228/human-gate)**: 2026-08-02 の行に含まれる部品の 1 つで、agent の承認ゲートのための rule と hook です。外した足場の例として、凍結した状態で公開しています。
- **[shimo4228](https://github.com/shimo4228/shimo4228)**: 著者の hub です。5 つの長期プロジェクトと DOI があります。

## ライセンス

MIT。[`LICENSE`](LICENSE) を参照してください。

<details>
<summary>ツールと AI アシスタント向けの資料</summary>

harness-pruning は、1 つの個人用 Claude Code harness の退役台帳です。Architecture Decision Record（ADR）を持つ skill・rule・agent・hook・plugin・chain の段・執筆の規約の削除・ほかへの吸収・縮小をすべて日付つきで並べており、何を足すかは読んだが何を外すかを見たい、agent harness を作る人に向けています。

存在する理由は、harness engineering についての公開文書は harness に何を入れるべきかを論じる一方で、外したものを出典つきで見せている harness がほとんどないからです。この repository は公開された実例の 1 つで、主張でも推奨でもベンチマークでもありません。harness 1 つ、著者 1 人、tool 1 つで、比較対象はありません。

基本情報: MIT ライセンスです。中身は Markdown だけ（`README.md`、`README.ja.md`、`LEDGER.md`、`HOWTO.md`）で、コードも導入するものもありません。著者は Tatsuya Shimomoto（shimo4228）です。状態: harness からの同期ではなく手で編んでおり、台帳と件数は 2026-09-08 時点です。各行は著者の手元の harness の `~/.claude/docs/adr/` にある ADR を引用しており、それらの ADR はすべて claude-harness repository の `docs/adr/` で公開しています。ADR を残さずに行った削除は台帳の範囲外なので、件数は下限であって総数ではありません。

この記録が示すことと、この repository 自身の数値（2026-09-08 時点）: 台帳には退役イベントが 27 件あり、harness の ADR 64 件のうち 27 件にあたります。残る 37 件は退役ではない決定の記録です。harness の全履歴で skill は 127 件作られ 68 件削除されたので（`skills/*/SKILL.md` のパス数）、パス数で数えると harness は小さくなったのではなく入れ替わりました。削除 1 件あたりの追加は skill 層でおよそ 1.9 件、agent 層と rule 層で 1.5 件です。27 行のうち 14 行の退役には、部品の役目を harness の外にあるものが引き受けるという方向性があります。27 行のうち 7 行がモデル世代を名指しし、4 行が名指しせず世代交代に帰しています。"not model-attributed" の 16 行のうち、3 行は substrate（built-in・tool・公式の既定）を名指しし、13 行は重複・不使用・スクリプトへ移した機械的な検査など harness の内側にある理由を挙げています。

リンク: [LEDGER.md](LEDGER.md)（英語）が net change 節つきの台帳、[HOWTO.md](HOWTO.md)（英語）が退役の判断のしかたの要約で、harness の Scaffold Dissolution の原則（rule は足場で、それなしで実践が回るようになったら簡素化するか削除する）、generation-audit の手順、実例 1 件から成ります。引用している ADR は [claude-harness/docs/adr](https://github.com/shimo4228/claude-harness/tree/main/docs/adr) にあります。Scaffold Dissolution は [Agent Knowledge Cycle](https://github.com/shimo4228/agent-knowledge-cycle)（concept DOI、つまり常に最新版へつながる代表 DOI [10.5281/zenodo.19200726](https://doi.org/10.5281/zenodo.19200726)）の一部です。著者の hub は [shimo4228/shimo4228](https://github.com/shimo4228/shimo4228) です。

</details>
