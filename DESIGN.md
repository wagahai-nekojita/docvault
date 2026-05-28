# docvault design

docvault は、雑メモを人間が事前分類せず `inbox/` に投げ、エージェントが軽く整えて Filed Note にするための Git-backed inbox-zero vault です。目的は文書管理アプリを作ることではなく、判断を policy として明示し、実行と履歴を標準部品へ寄せることです。

## Problem

個人メモは、保存時に分類を求めるほど破綻しやすくなります。一方で、旧版を手で残すと working tree が散らかります。docvault は Capture を先に受け取り、Processing Run の判断を Git diff で確認する形に寄せます。

## Principles

- policy / mechanism separation: 分類、校正、命名、schema は policy として記述し、履歴と差分は Git に任せる。
- anti-additive: 困っていない機構は足さない。予約席は製品名ではなく能力名で書く。
- capture-first: 人間は `inbox/` に入れるだけにする。事前のフォルダ判断を要求しない。
- safe-zone: v1 の agent 編集は Inbox と単一の filing move に限定する。Filed Note は linkable and stable と扱う。
- staged scope: v1 は inbox-zero、v2 は compilation。

## Adopt / Reserve / Ignore

| Verdict | Capability | Reason |
| --- | --- | --- |
| Adopt now | Markdown | 保存形式として十分に durable。 |
| Adopt now | Git | 旧版、差分、レビュー、rollback を substrate として担う。 |
| Adopt now | YAML frontmatter | note metadata を本文と同居させる軽い契約。 |
| Adopt now | JSON Schema as contract | 自動検証ではなく、frontmatter の明示 contract として採用する。 |
| Adopt now | `AGENTS.md` | agent runtime に渡す処理 policy の置き場。 |
| Adopt now | exchangeable agent runtime | `AGENTS.md` と Git を扱える runtime なら差し替え可能にする。 |
| Reserve | capture sync mechanism | 別端末からの Capture が週3回以上になったら選ぶ。 |
| Reserve | schema validation mechanism | frontmatter の schema 逸脱が2回以上レビューで見つかったら選ぶ。 |
| Reserve | wikilink-aware vault tool | agent に Filed Note の rename、move、refactor、link repair を任せたくなったら選ぶ。 |
| Reserve | prose linting mechanism | 同じ種類の校正ミスが2回以上 Processing Run をすり抜けたら選ぶ。 |
| Reserve | compilation mechanism | inbox-zero が2週間安定し、横断 synthesis を手で作り始めたら選ぶ。 |
| Ignore in v1 | custom classify/repair scripts | policy を増やす前に自作 mechanism を増やさない。 |
| Ignore in v1 | permanent MCP stack | v1 の safe-zone では常設する必要がない。 |
| Ignore in v1 | broad lint pipeline | 実害が出るまで導入しない。 |
| Ignore in v1 | active link graph maintenance | Filed Note を agent が触らないことで回避する。 |
| Ignore in v1 | filed-note refactoring | wikilink-aware vault tool 採用まで対象外。 |

## v1 Repository Shape

v1 で作るものは、短い README、判断記録の DESIGN、agent policy の AGENTS、frontmatter contract、Inbox と Filed Note の置き場だけです。自動 validation、同期、compilation は昇格条件が満たされるまで入れません。
