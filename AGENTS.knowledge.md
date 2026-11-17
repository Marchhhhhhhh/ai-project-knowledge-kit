# Project Knowledge Protocol

This is a generic rule set intended to be merged into a target project's root `AGENTS.md`. It governs how project knowledge is recorded, discussed, and archived. It does not contain product-specific design or technical rules.

## Project Knowledge Management

### Core Principles

- Preserve long-term memory in project-local text so that future contributors and agents can understand context, conclusions, and trade-offs rather than seeing only final outcomes.
- Discuss and confirm ideas before archiving them. Do not generate records merely to complete a workflow when no clear conclusion exists.
- Archive knowledge when it serves a real understanding need; not every conversation or review requires a record.
- Each project may add its own development, product, and operational rules alongside this protocol. Those project-specific rules are not part of this generic protocol.

### At the Start of a Discussion: Check the Draft Inbox

- At the beginning of a project discussion, check `Drafts/` for unprocessed ideas and `Progress/Progress.md` for their pending status.
- If pending ideas exist, tell the user and confirm whether this session should address them. Do not treat every draft as authorization for immediate implementation.
- A new request raised directly in the current conversation does not need to be paused or rewritten merely to match an existing draft.

### Drafts: Preserve Authentic, Unrefined Input

- Use `Drafts/` for fragmented ideas, questions, and requests. The recommended filename format is `YYYYMMDD_sequence.md`; one file may contain multiple topics.
- Drafts capture authentic input from before a discussion. They may include uncertainties, images, and immature ideas; they do not need to be complete proposals.
- A draft is neither a commitment nor confirmation. Undiscussed and unconfirmed portions remain pending in the draft inbox.
- One draft may be discussed and archived over several sessions. Do not prematurely confirm unrelated topics just to mark the whole file as processed.

### Decision Records: Preserve Valid Conclusions and Their Rationale

- Once a discussion reaches a clear conclusion, archive information with long-term value in `Progress/`. The recommended filename is `YYYYMMDD_sequence-topic.md`; when a corresponding draft exists, its name should make that relationship recognizable.
- Use `Progress/TEMPLATE.md` as a reference. Each record should retain, as applicable:
  - source and date;
  - discussion origin or original request;
  - confirmed conclusions;
  - important reasoning, rejected alternatives, and why they were rejected;
  - effects on living documents, rules, or implementation.
- Record not only why an option was chosen, but also why alternatives were not chosen. This prevents repeated debate and silent reversals after the original context is forgotten.
- Records may distinguish “confirmed, pending implementation” from “implemented.” Design consensus is not implementation verification and must not be presented as a substitute for tests or acceptance checks.
- Optimize records for readability and traceability rather than mechanically filling every section. Empty sections may be removed.

### Conclusions from Direct Conversation: Archive Proactively, Never Fabricate Drafts

- When a discussion has no corresponding `Drafts/` entry and reaches a clear conclusion, the agent should archive it proactively without waiting for a separate user request. Do not require a draft to be written afterward.
- Such a record must include a “Discussion Origin” section that summarizes or quotes the user's original request, preserving the path from initial idea to conclusion.
- In `Progress/Progress.md`, mark the source as “No corresponding draft; raised directly in conversation.” Do not leave the source blank or link to a nonexistent draft.

### Status Index: Maintain Only Essential Navigation

- Update `Progress/Progress.md` whenever a record is added or materially updated.
- The index records source, archive file, current status, update date, and necessary context. Keep detailed reasoning in the record itself to avoid maintaining two full copies.
- When only part of a draft has been processed, identify the relevant topic in the index. Do not mark the entire draft as processed.
- Status values should describe reality, such as “confirmed, pending implementation,” “implemented,” or “amended by a later decision.” Status may be updated after implementation without erasing the original design rationale.

### Living Consensus and Decision History: Maintain Separately

- `Progress/` preserves time-specific decision history. Project-designated living documents describe the consensus currently in effect.
- Each project chooses its living documents. They may be `README.md`, architecture documents, or other existing documents; no particular filename or new document is mandatory.
- When an archived conclusion affects current design, rules, or ways of working, synchronize the relevant living documents. If a living document conflicts with a valid decision, identify the conflict and coordinate a correction rather than silently maintaining contradictory guidance.
- When a new decision amends an old one, add a record explaining the amendment and update the old record's status or index entry where useful. Do not silently rewrite history to make the old conclusion appear never to have existed.

### Archiving Boundaries: Do Not Turn the Workflow into Noise

- Valuable records include product-design consensus, architectural or reliability trade-offs, interaction rules, process rules, and other decisions that affect future understanding or implementation.
- Routine code reviews, test runs, daily operations, and troubleshooting do not need Progress records when they are clean or produce no new conclusion. Keep their evidence in the original test, review, or operational logs.
- If such an activity produces a reusable rule or new consensus, archive only that conclusion and the context needed to understand it, rather than copying the entire activity log.
- Ordinary implementation details already expressed clearly in code, tests, or commits do not require separate decision records.

### Project-Specific Extensions

- Existing `AGENTS.md`, README files, testing requirements, startup procedures, and business rules in the target project remain effective. Merge this protocol into them; do not overwrite or delete them.
- A project may define its living-document locations, draft naming conventions, and supplementary rules, but it should not weaken the core semantics of authentic input, explicit conclusions, traceable history, proactive archiving, and noise control.
