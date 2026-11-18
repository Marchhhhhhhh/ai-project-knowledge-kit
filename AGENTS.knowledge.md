# Project Knowledge Protocol

This is a generic rule set intended to be merged into a target project's root `AGENTS.md`. It governs how project knowledge is recorded, discussed, and archived. It does not contain product-specific design or technical rules.

## Project Knowledge Management

### Core Principles

- Preserve long-term memory in project-local text so that future contributors and agents can understand context, conclusions, and trade-offs rather than seeing only final outcomes.
- Discuss and confirm ideas before archiving them. Do not generate records merely to complete a workflow when no clear conclusion exists.
- Archive knowledge when it serves a real understanding need; not every conversation or review requires a record.
- Each project may add its own development, product, and operational rules alongside this protocol. Those project-specific rules are not part of this generic protocol.
- “The user” means the person accountable for the current project or decision. In team projects, use the established owner or approval process; when no owner is clear, ask rather than assuming that any participant can confirm every decision.

### At the Start of a Discussion: Check the Draft Inbox

- At the beginning of a project discussion, check `Drafts/` for unprocessed ideas and `Progress/Progress.md` for their pending status.
- If pending ideas exist, tell the user and confirm whether this session should address them. Do not treat every draft as authorization for immediate implementation.
- A new request raised directly in the current conversation does not need to be paused or rewritten merely to match an existing draft.

### Drafts: Preserve Authentic, Unrefined Input

- Use `Drafts/` for fragmented ideas, questions, and requests. For personal or low-concurrency use, the recommended filename is `YYYYMM.md`; for parallel collaboration, use `YYYYMM_author.md` with a stable team account or author identifier so contributors can number independently and avoid shared-file conflicts.
- Within a monthly file, group entries under `YYYY-MM-DD` headings and number them `01`, `02`, and so on within that date, with a short topic heading. The date is when the entry was captured, not when the idea first occurred. Numbers remain stable: do not renumber, rearrange, or move unresolved entries into a new month after discussion or archiving. Source references identify the file, entry date, number, and topic scope.
- Preserve the author's original wording. When an agent captures an idea or receives a draft without the recommended metadata, use the actual capture date, append the next number within that date, and add a short heading without requiring the author to rewrite the input. Never infer an earlier idea date from file timestamps. For historical material, use the actual import date and identify it as imported on that date, or state that its original date is unknown.
- Legacy `Drafts/YYYYMMDD_sequence.md` files and their Source references remain valid. Do not rename or rewrite them merely to adopt monthly drafts; a project may choose a different deliberate convention as long as entries remain stably identifiable and traceable.
- Drafts capture authentic input from before a discussion. They may include uncertainties, images, and immature ideas; they do not need to be complete proposals.
- A draft is neither a commitment nor confirmation. Undiscussed and unconfirmed portions remain pending in the draft inbox.
- One monthly file may contain topics discussed and archived over several sessions and across later months. Do not prematurely confirm unrelated topics just to mark the whole file as processed. The index, rather than the newest monthly file, determines pending work.
- When a new draft entry is added, also add its pending topics to `Progress/Progress.md`. Use `—` in the Record column until a decision record exists, and use the status `Pending discussion`. This makes pending work discoverable without inventing a conclusion or an archive file.

### Confirmation: The Accountable Human Decides

- “Confirmed” means that the user or another human decision-maker accountable for the project has explicitly accepted a specific conclusion or chosen an option. An agent's summary, recommendation, or inference of agreement is not confirmation by itself.
- Before archiving, check that the confirmed scope is unambiguous: which topic, option, and constraints were accepted, and which questions remain open. If this is unclear, present a concise proposed conclusion and ask for confirmation rather than archiving it as settled.
- Once the user has explicitly confirmed a conclusion, the agent does not need to ask again for permission to archive it. Proactive archiving means initiating the record-keeping step, not unilaterally approving a proposal.
- An agent may archive a decision made by another accountable person when that decision is clearly documented. Routine editorial clarification may be performed without new approval, but any substantive change to a conclusion requires renewed confirmation.

### Decision Records: Preserve Valid Conclusions and Their Rationale

- Archiving means **creating a new decision record in `Progress/`, preserving the original draft and any unconfirmed topics, and updating `Progress/Progress.md`**. It does not mean moving, deleting, or rewriting the original draft.
- Once a discussion reaches a clear, human-confirmed conclusion, archive information with long-term value in `Progress/`. The recommended filename is `YYYYMMDD_sequence-topic.md`: use the archive date and the sequence number of that record within that date. The Source field and source metadata establish the relationship with a draft; do not reuse the draft's filename as a substitute for the record's own date and sequence.
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

- When a discussion has no corresponding `Drafts/` entry and reaches a clear, human-confirmed conclusion, the agent should archive it proactively without waiting for a separate user request. Do not require a draft to be written afterward.
- Such a record must include a “Discussion Origin” section that summarizes or quotes the user's original request, preserving the path from initial idea to conclusion.
- In `Progress/Progress.md`, mark the source as “No corresponding draft; raised directly in conversation.” Do not leave the source blank or link to a nonexistent draft.

### Status Index: Track Pending Topics and Decision Records

- Update `Progress/Progress.md` when a draft entry is added, when a decision record is added or materially updated, or when a topic's processing status changes.
- The index serves both pending work and decision history. A pending topic uses its draft as the Source, `—` as the Record, and the status `Pending discussion`. Replace `—` with the record path only after a human-confirmed decision has been archived.
- The index records source, optional record path, current status, update date, and necessary context. Keep detailed reasoning in the record itself to avoid maintaining two full copies.
- When only part of a draft has been processed, keep the unconfirmed topics pending and add a separate row for each newly archived decision. Each row must identify its topic scope; do not mark the entire draft as processed.
- The same rule applies within a single topic: if only one question or sub-scope is confirmed, split the remaining open question into its own pending row with a precise Source scope. Do not bury it only in a confirmed record's Notes or assume that a decision on the parent topic resolves it. Link that pending row to a decision record only when the open question itself has been explicitly resolved.
- A decision to reject or defer a topic is also a confirmed conclusion, not an unresolved topic. Archive the decision and its rationale, link the index row to that record, and use the exact status `Rejected` or `Deferred`. Do not leave a human-decided “do not do this” or “not now” item indefinitely marked as pending.
- Use these exact status values and capitalization: `Pending discussion`, `Confirmed, pending implementation`, `Implemented`, `Rejected`, `Deferred`, and `Amended by a later decision`. Status may be updated after implementation without erasing the original design rationale. A later human decision may reopen a rejected or deferred topic by creating a new record and adding a new index row for the newly confirmed scope. Change the old `Rejected` or `Deferred` row to `Amended by a later decision` and identify the new record in its Notes; preserve the old record itself rather than silently changing its conclusion.

### Living Documents and Decision History: Maintain Separately

- `Progress/` preserves time-specific decision history. Project-designated living documents describe the consensus currently in effect.
- Each project chooses its living documents. They may be `README.md`, architecture documents, or other existing documents; no particular filename or new document is mandatory.
- Living documents must distinguish current behavior from approved future behavior. A confirmed but unimplemented decision may be added only in a clearly labeled section such as “Approved, not yet implemented,” with a link to its decision record. Do not describe it in present tense as existing behavior, and do not mix it into instructions that readers would reasonably interpret as already usable.
- After implementation and verification, update the living documents to describe the behavior as current, remove the pending label, and update the record and index status. If implementation intentionally differs from the approved design, obtain confirmation for the substantive difference and record the amendment.
- When an archived conclusion affects current design, rules, or ways of working, synchronize the relevant living documents using the distinction above. If a living document conflicts with a valid decision, identify the conflict and coordinate a correction rather than silently maintaining contradictory guidance.
- When a new decision amends an old one, add a record explaining the amendment and update the old record's status or index entry where useful. Do not silently rewrite history to make the old conclusion appear never to have existed.

### Archiving Boundaries: Do Not Turn the Workflow into Noise

- Valuable records include product-design consensus, architectural or reliability trade-offs, interaction rules, process rules, and other decisions that affect future understanding or implementation.
- Routine code reviews, test runs, daily operations, and troubleshooting do not need Progress records when they are clean or produce no new conclusion. Keep their evidence in the original test, review, or operational logs.
- If such an activity produces a reusable rule or new consensus, archive only that conclusion and the context needed to understand it, rather than copying the entire activity log.
- Ordinary implementation details already expressed clearly in code, tests, or commits do not require separate decision records.

### Protocol Provenance and Upgrades

- When this protocol is inlined from another repository, preserve the provenance comment immediately above it. It identifies the source location and the exact source commit SHA or distributed version used. This comment is operational metadata, not removable documentation noise.
- To upgrade, compare the recorded source version with the desired upstream version, review the protocol diff, and report effects on local customizations and existing workflows. Obtain the project owner's confirmation for substantive changes, then merge deliberately and update the provenance version. Never overwrite the whole `AGENTS.md` during an upgrade.

### Project-Specific Extensions

- Existing `AGENTS.md`, README files, testing requirements, startup procedures, and business rules in the target project remain effective. Merge this protocol into them; do not overwrite or delete them.
- A project may define its living-document locations, draft naming conventions, and supplementary rules, but it should not weaken the core semantics of authentic input, explicit conclusions, traceable history, proactive archiving, and noise control.
