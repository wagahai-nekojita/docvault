# docvault

docvault は、個人の Markdown メモを `inbox/` に集め、エージェントが整理し、Git diff で判断を確認するための inbox-zero vault です。

## Why this exists

Notion や Obsidian のような文書管理ツールは、多くの人にとって便利です。でも、保存するたびに分類、命名、形式、置き場所を考える必要があると、それだけで続かない人もいます。メモは散らかり、フォーマットはばらばらになり、後から探すことも難しくなります。

docvault は、その負担を人間から外すための実験です。人間がやることは、メモ、記事の抜粋、スクリーンショットから拾った文章、思いつきを Markdown Capture として `inbox/` に置くことだけです。その後の軽い校正、frontmatter、分類、命名、移動は agent に任せます。

ただし、判断を見えなくするための仕組みではありません。agent の処理結果は Git diff に残し、人間は「何がどう整理されたか」だけを確認します。これは完成した文書管理アプリではなく、まず散らかった情報を安全に受け止め、後から見直せる形にするための vault skeleton です。

v1 は Markdown Capture の inbox-zero に限定しています。ノート横断の要約、リンク整理、同期、画像そのものの管理は、必要になった時点で別の能力として扱います。

## 30秒で分かる流れ

1. 雑メモを Markdown の Capture として `inbox/` に入れる。
2. エージェントが `AGENTS.md` に従って Processing Run を行う。
3. ユーザーが Git diff で校正、frontmatter、分類、移動先を確認する。
4. 問題なければ main に取り込む。

## Quickstart

まず、次のような Markdown ファイルを `inbox/` に置きます。ファイル名は仮で構いません。記事やスクリーンショットを扱う場合も、v1 ではいったん Markdown Capture として貼り付けます。

```md
Capture Date: 2026-06-06

Title: Inbox-first note handling

Putting raw notes into one inbox first reduces the need to decide the final folder at capture time.
The filing decision can happen later, when the note is reviewed with more context.
```

例:

```text
inbox/try-docvault.md
```

次に agent にこう頼みます。

```text
inbox/ を Processing Run してください。
```

agent は通常、作業ブランチ `codex/inbox-YYYY-MM-DD` を作り、Capture を軽く校正し、frontmatter を付け、`notes/projects/`、`notes/references/`、`notes/journal/`、または `archive/` に移します。判断できないものは `inbox/` に残し、`status: needs-review` と `review_note` だけを付けます。機密情報、認証情報、金融情報、本人確認情報を含む Capture は完全に触らず、commit に含めません。

レビューでは、主に次を見ます。

```sh
git diff --stat
git diff --name-status
git diff
```

- Capture が期待した移動先に移ったか。
- `title`、`created`、`type` が意図に合っているか。
- `created` とファイル名の日付が Capture Date と一致しているか。
- 本文が軽く整えられているだけで、意味や声が変わっていないか。
- `processing-log.md` に filed または archived note だけが1行追記されているか。
- sensitive な Capture が変更、stage、commit されていないか。

## Capture Date

Capture Date は、Capture が vault に入った日付です。本文で扱っている出来事の日付とは限りません。

Capture の先頭付近に、次の形式で明示してください。

```text
Capture Date: YYYY-MM-DD
```

Filed Note になった後は、この日付が frontmatter の `created` とファイル名の `YYYY-MM-DD-<slug>.md` に使われます。たとえば `Capture Date: 2026-06-06` なら、`created: 2026-06-06` と `2026-06-06-inbox-first-note-handling.md` が一致していることを diff で確認します。

Capture Date が曖昧な場合、agent は無理に分類せず `status: needs-review` にします。

## Schema と needs-review

`schema/note.schema.json` は Filed Note の frontmatter contract です。つまり、`notes/` や `archive/` に移された note は `title`、`created`、`type` を持ちます。

一方、`status: needs-review` の Capture はまだ Filed Note ではありません。`inbox/` に残る一時状態なので、`status: needs-review` と `review_note` だけでも policy 上は有効です。Filed Note 用 schema を `inbox/` の needs-review Capture にそのまま当てる必要はありません。

## Documents

- [DESIGN.md](DESIGN.md): なぜこの形にしたか。
- [AGENTS.md](AGENTS.md): agent が inbox を処理するときの policy。
- [examples/](examples/): Processing Run の判断境界を示す非運用の Example Case。Capture ではなく、Processing Run では処理しません。
- [schema/note.schema.json](schema/note.schema.json): Filed Note の frontmatter contract。
- [CONTEXT.md](CONTEXT.md): この repo で使う用語。

## Scope

v1 は inbox-zero に限定します。ノート横断の compilation は、inbox-zero が安定してから v2 で扱います。
