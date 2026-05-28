# docvault

docvault は、個人の Markdown メモを `inbox/` に集め、エージェントが整理し、Git diff で判断を確認するための inbox-zero vault です。

## Intent

これは個人的な実験用途の vault skeleton です。ドキュメント管理が苦手で、まず生メモを安全に受け止めてから整理したい人の参考になることを意図しています。

## 30秒で分かる流れ

1. 雑メモを Markdown の Capture として `inbox/` に入れる。
2. エージェントが `AGENTS.md` に従って Processing Run を行う。
3. 人間が Git diff で校正、frontmatter、分類、移動先を確認する。
4. 問題なければ main に取り込む。

## Documents

- [DESIGN.md](DESIGN.md): なぜこの形にしたか。
- [AGENTS.md](AGENTS.md): agent が inbox を処理するときの policy。
- [schema/note.schema.json](schema/note.schema.json): Filed Note の frontmatter contract。
- [CONTEXT.md](CONTEXT.md): この repo で使う用語。

## Scope

v1 は inbox-zero に限定します。ノート横断の compilation は、inbox-zero が安定してから v2 で扱います。
