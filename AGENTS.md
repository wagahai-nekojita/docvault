# AGENTS.md - docvault processing policy

This repository is a personal Markdown vault. Raw Captures are placed in `inbox/`. When asked to process the Inbox, run one bounded Processing Run: lightly clean Captures, add frontmatter, classify, name, file, and make the decisions reviewable through Git.

Do not write scripts. Act directly on files according to this policy.

## Processing Run

Before changing files, use a branch named `codex/inbox-YYYY-MM-DD`. Never commit directly to `main`.

For each `inbox/*.md` Capture not marked with parseable `do-not-process: true`:

1. If the Capture contains secrets, credentials, financial data, or identity data, leave the body untouched in `inbox/`, do not stage or commit that file, and report it as left uncommitted.
2. If the Capture cannot be safely filed because classification, format, metadata, or intent is unclear, leave the body untouched, add or update only frontmatter with `status: needs-review` and a one-line `review_note`, and keep it in `inbox/`.
3. Otherwise, proofread lightly. Fix typos, punctuation, and inconsistent notation. Preserve the author's meaning and voice. Do not summarize, expand, or invent facts.
4. Add YAML frontmatter matching `schema/note.schema.json`.
5. Set `created` to the Capture Date. The filename date and `created` value must match.
6. Classify the Filed Note as `project`, `reference`, `journal`, or `archive`.
7. Rename the file to `YYYY-MM-DD-<slug>.md`, where `<slug>` is short ASCII kebab-case derived from the title.
8. Move it to the selected destination.
9. Append one Processing Log line only for filed or archived notes: `- YYYY-MM-DD old/path.md -> new/path.md (type)`.

One normal Processing Run produces one commit with message `inbox: filed <n> notes`. Sensitive Captures are excluded from staging and commit.

## Classification

- Specific active project, person, commitment, or deadline -> `notes/projects/` with `type: project`.
- Durable knowledge, reusable principle, or reference -> `notes/references/` with `type: reference`.
- Dated personal log, diary-like entry, or fleeting thought -> `notes/journal/` with `type: journal`.
- Complete, obsolete, or removed from active reference -> `archive/` with `type: archive` and `status: archived`.

If you cannot choose confidently, do not guess. Use `status: needs-review` and a one-line `review_note`.

## Frontmatter Rules

- Required fields: `title`, `created`, `type`.
- Optional `status` values: `needs-review`, `processed`, `archived`.
- Optional `tags`: one to three lowercase ASCII kebab-case strings with evidence in the Capture.
- Optional `source`: use only when the Capture explicitly names a URL, book, meeting, person, or imported note system.
- `do-not-process: true` means leave the file completely untouched if the frontmatter is parseable.

## Safe Zone

During a Processing Run, you may edit only:

- Inbox Captures under `inbox/`.
- The single move of an Inbox Capture to `notes/` or `archive/`.
- Append-only entries in `processing-log.md`.

Do not edit `README.md`, `DESIGN.md`, `CONTEXT.md`, `AGENTS.md`, `schema/note.schema.json`, existing Filed Notes, or existing Archived Notes during a Processing Run.

## Never

- Never process non-Markdown Captures as Filed Notes.
- Never use a generic `note` type.
- Never use `status: inbox`.
- Never create custom classify, repair, rename, validation, or sync scripts.
- Never install or depend on permanent MCP servers for v1 inbox processing.
- Never rename, move, or refactor existing Filed Notes.
