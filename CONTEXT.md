# Docvault

Docvault is a Git-backed inbox-zero vault for personal documents. It exists to turn raw captures into filed notes while keeping every filing decision reviewable.

## Language

**Capture**:
A raw Markdown note that has been dropped into the vault before filing. A Capture may be rough, incomplete, or unclassified, but v1 Captures are always `.md` files.
_Avoid_: Draft, source document, input file

**Inbox**:
The temporary holding area for Captures that have not yet been filed. The Inbox is the only place where unprocessed material is expected to accumulate, and it is the only area where Captures are routinely changed by an agent.
_Avoid_: Staging area, queue, unsorted folder

**Filed Note**:
A Capture that has been proofread lightly, given metadata, named, and placed into its long-lived location. A Filed Note preserves the author's original meaning and voice; it is not a synthesized article or expanded explanation. Once filed, it is treated as linkable and stable.
_Avoid_: Processed file, clean note, final document

**Note Type**:
The primary category assigned to a Filed Note: Project Note, Reference Note, Journal Note, or Archived Note. A Note Type is never a generic "note"; uncertainty is handled as Needs Review.
_Avoid_: Folder type, document kind

**Capture Date**:
The date a Capture entered the vault. Capture Date is operational metadata, not necessarily the date of the event described by the Capture. A Filed Note's `created` metadata and filename date both use the Capture Date.
_Avoid_: Event date, written date

**Tag**:
A small, evidence-backed search hint attached to a Filed Note. Tags supplement the Note Type; they do not replace classification.
_Avoid_: Category, topic hierarchy, label taxonomy

**Source**:
An explicit origin named inside a Capture, such as a URL, book, meeting, person, or imported note system. A Source is omitted when the origin is not stated.
_Avoid_: Assumed origin, citation guess

**Project Note**:
A Filed Note tied to a specific active project, person, commitment, or deadline.
_Avoid_: Task note, work note

**Reference Note**:
A Filed Note that captures durable knowledge, a reusable principle, or a source-independent reference.
_Avoid_: Knowledge article, wiki page

**Journal Note**:
A Filed Note that records a dated personal log, diary-like entry, or fleeting thought.
_Avoid_: Daily note, scratch note

**Archived Note**:
A filed document that is preserved for history but removed from the active note set because it is complete, obsolete, or no longer useful for current reference.
_Avoid_: Deleted note, cold storage

**Processing Run**:
One bounded pass where an agent reviews Captures, decides what can be filed, and leaves ambiguous or sensitive material visible for human review. A Processing Run is reviewed as a single unit.
_Avoid_: Batch job, automation, import

**Processing Log**:
A lightweight human-readable list of filing actions produced during Processing Runs. The Processing Log is an index for review, not the authoritative history.
_Avoid_: Audit log, changelog, decision record

**Needs Review**:
The state of a Capture that the agent cannot safely file because classification, sensitivity, format, metadata, or intent is unclear. Needs Review is an explicit outcome, not a failure.
_Avoid_: Error, failed processing, skipped file

**Do Not Process**:
A user's explicit instruction that a Capture must be left untouched during a Processing Run. Do Not Process is separate from Needs Review because no agent judgment is being requested.
_Avoid_: Skip, ignore, archived

## Example Dialogue

**User**: "I dropped three Captures into the Inbox. Can you process them?"

**Agent**: "Two became Filed Notes. One is marked Needs Review because it mentions account details and I cannot safely classify it."
