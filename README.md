# docvault

docvault is a Git-backed inbox-zero vault skeleton for raw Markdown notes. This public repository is a distributable skeleton: docs, policy examples, schema, empty directories, and synthetic samples are public, while real Captures, real Filed Notes, and private attachments belong in a user's Private Vault Instance. Real user data belongs in a Private Vault Instance, not in the Public Skeleton.

## Why this exists

Most note systems ask you to decide the folder, name, metadata, and cleanup style at the moment you capture an idea. docvault moves those decisions into a bounded Processing Run. You provide raw text as a Capture, and the agent lightly proofreads it, adds frontmatter, classifies it, renames it, and files it without hiding the decision trail.

v1 is intentionally narrow: Markdown Captures in, reviewable Filed Notes out.

See [DETAILS.md](DETAILS.md) for the operational boundary between this Public Skeleton and a Private Vault Instance.

## 30-second flow

1. Paste or place raw text as a Capture.
2. Ask an agent to process the Inbox under [AGENTS.md](AGENTS.md).
3. Review the changed files with Git diff.
4. Keep filed notes, or revise anything marked Needs Review.

## Quickstart

Primary path: paste this into a chat session with your agent.

```text
このメモを Capture として inbox に入れて、処理して
---
ここに生メモ本文
```

The pasted text is first created or treated as a Capture in `inbox/`. Only after that does the Processing Run policy apply: the agent checks for sensitive material, adds metadata when safe, classifies the note, moves Filed Notes into `notes/` or `archive/`, and leaves unclear material in `inbox/` as Needs Review.

Alternate file-based path: create `inbox/try-docvault.md`, put raw Markdown in it, then ask:

```text
Process the inbox.
```

See [samples/notes/references/2026-06-06-inbox-first-note-handling.md](samples/notes/references/2026-06-06-inbox-first-note-handling.md) for a synthetic public Filed Note sample. It is completed output, not an `examples/` policy Example Case, and it does not publish private note content.

## More details

Read [DETAILS.md](DETAILS.md) for the public/private boundary, Capture Date, schema, Needs Review, review checklist, and Processing Log details.
