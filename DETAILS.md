# docvault details

This page holds operational detail that would make the README too long.

## Public and private boundary

This repository is a Public Skeleton for docvault. It is meant to distribute documentation, policy examples, schema, empty directories, and synthetic samples without publishing a user's live notes.

A Private Vault Instance is the user's local operating copy. Real Captures in `inbox/`, real Filed Notes in `notes/` or `archive/`, and private attachments belong in that private instance unless the user explicitly chooses to publish specific synthetic or approved material.

[examples/](examples/) contains non-operational policy cases. They show how Processing Run judgments should work, but they are not Captures and are never processed during a Processing Run.

[samples/](samples/) contains public synthetic examples of completed output. Samples can show the shape of a Filed Note without exposing recovered historical notes or private note bodies.

Local Operating State such as `.obsidian/`, `.codex-runs/`, root `GOAL.md`, and `goals/` supports a private local workflow. That state is not part of the Public Skeleton, and public documentation should not treat it as public repo content.

## Capture Date

Capture Date is the date a Capture entered the vault. It is operational metadata, not necessarily the date of the event described by the note.

When a Capture becomes a Filed Note, the Capture Date is used in two places:

```yaml
created: YYYY-MM-DD
```

```text
YYYY-MM-DD-<slug>.md
```

For example, a Capture Date of `2026-06-06` can become `notes/references/2026-06-06-inbox-first-note-handling.md` with `created: 2026-06-06`.

If the Capture Date is unclear, the agent should not guess. The Capture remains in `inbox/` as Needs Review.

## Schema

[schema/note.schema.json](schema/note.schema.json) is the frontmatter contract for Filed Notes in `notes/` and `archive/`.

Filed Notes require:

```yaml
title: Inbox-first note handling
created: 2026-06-06
type: reference
```

Allowed `type` values are `project`, `reference`, `journal`, and `archive`. Optional fields include `status`, `tags`, `source`, `do-not-process`, and `review_note`.

The schema is for Filed Notes. A Capture that remains in `inbox/` as Needs Review is not yet a Filed Note.

## Needs Review

Needs Review is the safe stopping state for a Capture the agent cannot file confidently. Typical reasons include unclear classification, missing or ambiguous Capture Date, uncertain intent, unsupported format, or possible sensitive content.

A Needs Review Capture stays in `inbox/` with only minimal frontmatter when needed:

```yaml
---
status: needs-review
review_note: Capture Date is unclear.
---
```

The body should stay untouched unless the policy explicitly allows otherwise. `do-not-process: true` is different: when parseable, it means the Capture must be left completely untouched.

## Review checklist

After a Processing Run, inspect the diff before keeping the result:

```sh
git diff --stat
git diff --name-status
git diff
```

Check that:

- Filed Notes moved to the expected destination.
- `title`, `created`, and `type` match the Capture.
- The filename date matches `created`.
- Body edits are light proofreading only.
- Ambiguous material stayed in `inbox/` as Needs Review.
- Sensitive Captures were not changed, staged, or committed.
- `examples/` files were not processed.

## Processing Log

[processing-log.md](processing-log.md) is an append-only review aid, not the authoritative history. Git remains the authoritative record.

Append one line only for each filed or archived Capture:

```text
- 2026-06-06 inbox/try-docvault.md -> notes/references/2026-06-06-inbox-first-note-handling.md (reference)
```

Do not add Processing Log lines for Needs Review Captures, sensitive Captures left untouched, `do-not-process: true` Captures, or files under `examples/`.

## Example Cases and Filed Note samples

[examples/](examples/) contains non-operational Example Cases. They illustrate policy boundaries and are never processed during a Processing Run.

[samples/](samples/) contains public synthetic samples of completed output. A sample Filed Note shows what a filed result can look like without using recovered personal notes.
