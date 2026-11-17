# Project Knowledge Kit

A **code-free, dependency-free** knowledge workflow for software projects. It separates raw ideas, confirmed decisions, decision history, and current project consensus so that contributors and AI agents can understand not only what was decided, but also why.

> **Core idea:** Preserve project memory in plain text, and use `AGENTS.md` to instruct agents how to maintain that memory.

Current distribution version: **0.1.0** (see [VERSION](VERSION)). Git-based integrations record the full source commit SHA; ZIP or copied-directory integrations record the source location and this version.

## 中文介绍

这是一套**项目知识沉淀模板包**，用于在其他项目中复用 `Drafts/`、`Progress/`、归档规则和 `AGENTS.md` 组成的工作流。它源自作者本地的 Work Bench 项目，不包含该项目的业务规则、真实草稿或历史决策。

- **Drafts（草稿箱）**：保留讨论前的真实想法，允许零碎、不成熟和一文多话题。
- **Progress/（决策记录目录）**：保存已经确认的结论、理由、否决项和后续修订关系。
- **Progress/Progress.md（状态索引文件）**：登记待处理话题并导航到决策记录，不重复完整论证。
- **AGENTS.knowledge.md（通用协议）**：由 Agent 内联合并进目标项目的 `AGENTS.md`，记录来源及完整提交号或分发版本，随后不保留第二份协议副本。
- **Living documents（当前共识文档）**：由目标项目指定，可以是已有 README、架构文档或产品文档，不强制新建。
- **确认权归人**：Agent 的提议或总结不等于确认；有决策权的人明确接受结论后，Agent 主动完成归档。
- **待处理事项可关闭**：新草稿及未决子项立即登记为 `Pending discussion`；明确不做或暂缓时分别归档为 `Rejected` 或 `Deferred`。
- **当前与未来分开**：已批准但尚未实现的内容不得写成现有行为，须放在明确的待实现分区。

模板包没有代码和运行时依赖。接入时必须保留目标项目已有内容，只创建缺失结构并合并协议，不能覆盖整个 `AGENTS.md` 或重写项目文档。本仓库自身不启用根 `AGENTS.md`，也不制造真实决策记录；`Progress/` 保持为空白模板。

本模板包以英文为主体；本节仅作中文简介，完整的接入步骤、Agent 提示词和日常使用规则见下文。

## Directory Contents

```text
ai-project-knowledge-kit/
├── README.md                 # This guide, including the Chinese introduction
├── AGENTS.knowledge.md       # Generic protocol to merge into a project's AGENTS.md
├── VERSION                   # Distribution version for non-Git integration and upgrades
├── LICENSE                   # MIT License for reuse and adaptation
├── .gitignore                # Minimal operating-system file exclusions
├── Drafts/
│   └── README.md             # Draft inbox guidance; copied by default, removable when redundant
└── Progress/
    ├── Progress.md           # Index template with no real project records
    └── TEMPLATE.md           # Reference template for a decision record
```

The template files contain no project-specific decisions, business rules, or personal information. Once copied into a project, its knowledge records evolve independently within that project.

This kit is distributed under the [MIT License](LICENSE). The directory tree identifies the default template payload; integration copies only the files explicitly listed below. Review reports, maintenance notes, and other repository-maintenance artifacts are not project templates.

## Terminology

- **Living documents（当前共识文档）** are the project-designated documents that describe consensus currently in effect, such as a README or architecture document. “Current project consensus” is the content they communicate, not a separate storage location.
- **Decision records（决策记录）** are dated files in `Progress/` that preserve conclusions and their context.
- **The status index（状态索引）** is `Progress/Progress.md`, not the entire `Progress/` directory.

## Workflow Overview

```text
Raw ideas in Drafts/ ──discussion──> confirmed conclusions ──archive──> Progress/
                                             │
                                             └──update──> Progress/Progress.md

Ideas raised directly in conversation ──discussion──> confirmed conclusions
                                             │
                                             └──archive──> Progress/

Conclusions that affect current rules ──sync──> the project's designated living documents
                                               (README, architecture docs, AGENTS.md, etc.)
```

For direct conversations, archive proactively after human confirmation and do not invent Drafts.

- **Drafts are inputs:** They may be incomplete, uncertain, or contain several topics. A draft is not a commitment to implement anything.
- **Archiving creates; it does not move:** After the user or another accountable human decision-maker explicitly accepts a conclusion, create a new decision record in `Progress/`, preserve the original draft and any unconfirmed topics, and update `Progress/Progress.md`. An agent's proposal or summary alone is not confirmation.
- **The index includes pending topics:** Add a new draft topic with `—` in the Record column and “Pending discussion” as its status. Replace the marker only when a confirmed decision has been archived.
- **Progress is history:** It preserves confirmed conclusions, including rejection and deferral decisions, reasoning, rejected alternatives, and later amendments.
- **Pending topics have an exit:** A human decision not to proceed or to postpone is archived and linked with the status `Rejected` or `Deferred`; it does not remain pending forever.
- **Living documents distinguish now from later:** They describe current behavior separately from approved but unimplemented decisions; they do not replace decision history.
- **The status index is navigation:** It helps locate drafts and records and understand their state without duplicating their full contents.

## Agent Integration in Another Project

Give the following request to an agent working in the target project, together with this repository's URL or local path:

> Read `README.md` and `AGENTS.knowledge.md` in the Project Knowledge Kit repository, and integrate this code-free knowledge workflow into the current project. Create only missing `Drafts/` and `Progress/` structures, including `Progress/TEMPLATE.md` and `Progress/Progress.md` with its header rules but no real project records; copy `Drafts/README.md` unless the project already covers its rules and deliberately retains the draft directory another way. Remove the illustrative comments from the copied index. Inline the generic protocol into the root `AGENTS.md` without overwriting existing content, recording the source repository URL or distribution location and the exact source commit SHA or distribution version immediately above the merged protocol. Then remove only the standalone `AGENTS.knowledge.md` copy introduced by this integration; preserve any pre-existing file with that name. Check for an existing knowledge or decision-recording workflow first, and surface any conflicts. Identify the project's living documents for current consensus. Copy only the template files listed in the integration steps, not maintenance artifacts such as `Docs/`. Do not copy illustrative examples as real project history or invent business decisions merely to populate the archive. When finished, report what was added, merged, preserved, the recorded protocol version, and any conflicts that require human judgment.

The integrating agent should follow these steps:

1. **Inspect the target project**
   - Read its existing `AGENTS.md`, README, contribution guides, and other agent instructions.
   - Check for existing `Drafts/`, `Progress/`, decision records, or archiving rules. Preserve and reconcile existing content rather than replacing entire directories.
2. **Copy only the blank template structure**
   - Create `Drafts/` and `Progress/` only when missing.
   - Copy `Drafts/README.md`, `Progress/Progress.md`, and `Progress/TEMPLATE.md`. Keeping the draft guide is the default because Git does not track empty directories and the guide explains pending-topic indexing and draft preservation. It may be omitted only when those rules are already covered by the merged `AGENTS.md` and the project has another deliberate way to retain `Drafts/`.
   - Copy `Progress/Progress.md` with its header rules and no real project records. Remove the illustrative HTML comments; do not erase the table or its instructions.
   - Do not copy real drafts, decisions, or images produced by this kit's use in any other project. Do not copy repository-maintenance artifacts such as `Docs/`.
3. **Inline the protocol as the single maintained copy**
   - Merge the contents of `AGENTS.knowledge.md` into the target project's root `AGENTS.md`. This repository's `.knowledge` suffix is only a staging convention for integration; it is not a file most agents will discover automatically.
   - Immediately above the merged protocol, add a provenance comment identifying the exact source used. For a Git source, use its repository URL and full commit SHA: `<!-- Project Knowledge Protocol source: https://github.com/OWNER/ai-project-knowledge-kit @ FULL_COMMIT_SHA -->`. For a ZIP or copied directory, use its location and the version in `VERSION`: `<!-- Project Knowledge Protocol source: DISTRIBUTION_LOCATION @ version 0.1.0 -->`. Replace every placeholder with the actual source information; do not record an unversioned branch name. Preserve this anchor during later upgrades.
   - After a successful inline merge, remove only the standalone `AGENTS.knowledge.md` copy introduced by this integration. Preserve any pre-existing file with that name until the user resolves its role. Do not leave both an inline copy and a referenced copy that can drift.
   - Preserve all unrelated project-specific rules. Do not delete or rewrite them merely to make the text look uniform.
   - If the project uses additional agent-instruction files, follow its existing convention for referencing the root `AGENTS.md` instead of creating several independently maintained copies.
   - A project that already centrally manages its agent instructions may keep an external reference instead of inlining only if its agent runtime actually follows that reference and the project explicitly chooses a single maintained source. Do not assume that merely mentioning a path activates it.
4. **Identify living documents**
   - Prefer existing README, architecture, product, or other current-consensus documents.
   - Do not require a new README or rewrite the project's design philosophy just to adopt this workflow.
5. **Perform lightweight verification**
   - Confirm that the new index retains its header rules and contains no invented drafts or decisions.
   - Confirm that the merged protocol covers startup draft checks, accountable-human confirmation, pending-topic and unresolved-sub-scope indexing, the three archiving actions, proactive archiving of direct conversations, record naming, rejection/deferral exits, later reopening, amendment history, current-versus-approved-future behavior, and noise control.
   - Confirm that the exact status spellings are preserved and that `Drafts/README.md` is present or its two key rules are covered elsewhere.
   - Confirm that the merged protocol has a provenance comment with the actual source location and either the full upstream commit SHA or the `VERSION` value used.
   - Report all file changes and any rule conflicts that need human resolution.

## Day-to-Day Use

### When an idea starts as a draft

Record it informally in `Drafts/`, and add each topic to `Progress/Progress.md` with `—` in the Record column and “Pending discussion” as its status. Discuss it with an agent or project collaborator. Different topics in one file may be confirmed separately.

“Confirmed” means that the user or another accountable human decision-maker has explicitly accepted a specific conclusion or option. An agent's proposal, summary, or interpretation of silence is not confirmation. If the accepted scope is unclear, ask before archiving.

Once a conclusion is confirmed, archiving consists of three actions: **create a new decision record in `Progress/`, preserve the original draft and its unconfirmed topics, and update the index**. Do not move or delete the original draft. Keep unconfirmed topics in separate pending rows; create a separate row for each archived decision.

This also applies to unresolved questions within one topic. If a decision confirms only part of the topic, add a pending row for each remaining open sub-scope rather than mentioning it only in the confirmed record's Notes. A pending sub-scope is resolved only by an explicit human decision; it is not implicitly approved or rejected by the parent topic's decision.

### When an idea starts in conversation

A draft is not required. After a human-confirmed conclusion emerges, the agent should proactively archive it without asking again for permission to perform the record-keeping step. Preserve the original motivation in a “Discussion Origin” section, and mark the index source as “No corresponding draft; raised directly in conversation.” Never backdate or fabricate a draft to make the workflow appear complete.

### When an idea is rejected or deferred

A decision not to implement an idea, or to postpone it, is a confirmed conclusion with an exit from pending work. Create a decision record explaining the rationale, link the topic's index row to it, and use the exact status `Rejected` or `Deferred`. Do not leave the row as `Pending discussion` merely because no implementation will occur.

If the topic is later reconsidered and accepted, create a new record and a new index row for the newly confirmed scope. Change the old `Rejected` or `Deferred` row to `Amended by a later decision`, identify the new record in its Notes, and preserve the old record's original conclusion. This reuses the existing amendment status; no separate `Reopened` status is needed.

### When a conclusion changes

Create a new record explaining which earlier decision is amended and why. Update the current living documents and, where useful, the old record's index status. Do not silently rewrite history so that the earlier conclusion appears never to have existed.

### When a decision is approved but not implemented

Do not describe the planned behavior as if it already exists. If it belongs in a living document before implementation, place it under a conspicuous heading such as “Approved, not yet implemented” and link to its decision record. Keep existing usage instructions and current-behavior descriptions unchanged. After implementation and verification, move the description into the current-behavior section, remove the pending label, and update the record and index status.

### After routine reviews or tests

If no reusable rule or new consensus emerged, do not create a Progress record. Existing test output, review logs, and commit history are sufficient. The workflow should reduce lost knowledge, not generate ceremonial documentation.

## Complete Fictional Example

The following example is entirely fictional. It illustrates file relationships and state transitions; it is not a real decision of this repository or a template to copy as project history.

### 1. Capture two topics without treating them as approved

Create `Drafts/20261117_01.md`:

```markdown
# Export format

Could we support both JSON and CSV exports?

# Notification timing

Should notifications be sent immediately or collected into a daily digest?
```

Record filenames use the archive date and that date's record sequence, not the source draft's date or sequence. The Source column establishes the draft relationship. The following dates intentionally differ across records.

Immediately index both undiscussed topics in `Progress/Progress.md`; there are no conclusions or decision records yet:

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/20261117_01.md (Export format) | — | Pending discussion | 2026-11-17 | JSON and CSV support not yet decided |
| Drafts/20261117_01.md (Notification timing) | — | Pending discussion | 2026-11-17 | Timing not yet decided |

### 2. Confirm and archive only the JSON scope

During discussion, an agent recommends supporting JSON first and postponing CSV. That recommendation alone is not confirmation. The user then explicitly replies, “Yes, use JSON only for the first version; CSV remains undecided.” The export-format topic is now confirmed within that specific scope.

Create `Progress/20261118_01-json-export.md`:

```markdown
# Decision Record: JSON Export for the First Version

- Source: `Drafts/20261117_01.md` (Export format)
- Archived: 2026-11-18
- Status: Confirmed, pending implementation

## Discussion Origin

The draft asked whether exports should support both JSON and CSV.

## Conclusions

The user explicitly approved JSON-only export for the first version. CSV support remains undecided rather than rejected permanently.

## Rationale and Trade-offs

JSON meets the current integration need without adding a second format before there is a concrete CSV use case.

## Impact on Current Consensus

Document JSON export as approved future behavior, not as an existing feature.

## Implementation and Verification

Implementation and verification have not started.
```

The original draft remains unchanged, including both topics. Update the index so the confirmed JSON scope points to its new record. Future CSV support becomes a separate pending sub-scope of Export format; it cannot exist only in the confirmed record's Notes. Notification timing also remains pending:

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/20261117_01.md (Export format — first-version JSON support) | Progress/20261118_01-json-export.md | Confirmed, pending implementation | 2026-11-18 | JSON approved for the first version |
| Drafts/20261117_01.md (Export format — future CSV support) | — | Pending discussion | 2026-11-18 | Explicitly left undecided by the user |
| Drafts/20261117_01.md (Notification timing) | — | Pending discussion | 2026-11-18 | Timing not yet decided |

If the README describes current application behavior, do not add “JSON export is available.” Instead, if advance documentation is useful, add a clearly separated section:

```markdown
## Approved, Not Yet Implemented

- JSON-only export has been approved for the first version.
  See `Progress/20261118_01-json-export.md`. It is not currently available.
```

### 3. Confirm another topic without resolving the CSV sub-scope

On a later date, the user explicitly chooses a daily digest for notifications. Create a second record, `Progress/20261119_01-daily-digest.md`, while preserving the same original draft. The index now contains two separate decision records, but future CSV support remains pending because the notification decision says nothing about it:

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/20261117_01.md (Export format — first-version JSON support) | Progress/20261118_01-json-export.md | Confirmed, pending implementation | 2026-11-18 | JSON approved for the first version |
| Drafts/20261117_01.md (Export format — future CSV support) | — | Pending discussion | 2026-11-19 | Still undecided; not resolved by the notification decision |
| Drafts/20261117_01.md (Notification timing) | Progress/20261119_01-daily-digest.md | Confirmed, pending implementation | 2026-11-19 | Send a daily digest; immediate notifications not approved |

Confirming notification timing does not rewrite the JSON record, resolve the CSV sub-scope, or imply that either confirmed feature has been implemented.

### 4. Resolve CSV and amend the export decision without erasing history

After implementation has begun, a real integration requirement makes CSV necessary. The agent does not silently change the old conclusion or treat CSV as having been approved earlier. It presents the new trade-off, and the user explicitly approves JSON and CSV together. This both resolves the pending CSV sub-scope and amends the earlier JSON-only decision.

Create a new record, `Progress/20261120_01-json-and-csv-export.md`, stating that it amends `Progress/20261118_01-json-export.md` and why. Replace the CSV pending row's `—` with the new record path and update its status. Update the living document to describe JSON and CSV as approved future behavior until both are implemented and verified. The index retains the old decision, the new decision, and the notification decision:

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/20261117_01.md (Export format — first-version JSON support) | Progress/20261118_01-json-export.md | Amended by a later decision | 2026-11-20 | JSON-only scope amended by 20261120_01-json-and-csv-export.md |
| Drafts/20261117_01.md (Export format — future CSV support) | Progress/20261120_01-json-and-csv-export.md | Confirmed, pending implementation | 2026-11-20 | CSV explicitly approved; JSON and CSV now form the approved export scope |
| Drafts/20261117_01.md (Notification timing) | Progress/20261119_01-daily-digest.md | Confirmed, pending implementation | 2026-11-19 | Send a daily digest; immediate notifications not approved |

The original draft and both export records remain available. The old record shows what was approved at that time, the pending CSV row tracked the unresolved sub-scope until its explicit resolution, and the new record shows the current approved direction. The README continues to distinguish approved future behavior from verified existing behavior.

## Maintenance and Evolution

- The first version is plain text: no installer, initialization script, synchronization process, or runtime dependency.
- Projects may adapt copied templates to local needs. Copies are not automatically synchronized across projects.
- Each inlined protocol carries a source location and an exact upstream commit SHA or distribution version. Git sources use the full commit SHA; ZIP and copied-directory sources use the value in `VERSION`. To upgrade, compare the recorded version with the desired upstream version and review the protocol diff; report the effects on local customizations and existing workflows; obtain the project owner's confirmation for substantive changes; then merge deliberately and update the provenance version. Never overwrite the whole `AGENTS.md` during an upgrade.
- When publishing a changed distribution, update `VERSION` and the matching version references in this README in the same change. Git tags are optional; the version file is the portable reference for non-Git consumers.
- The generic protocol describes only the knowledge workflow. Coding, testing, release, and business rules remain in each project's own `AGENTS.md`.
- CLI tooling, version checks, and automatic synchronization should be considered only when real use in actual projects reveals a concrete need. They are not assumed to be inevitable next steps.

## Using This Kit to Maintain Itself

This kit repository intentionally has no root `AGENTS.md` and does not maintain real project decision records in its template `Progress/`. It is a protocol source, not a business project; the template files must remain free of repository-maintenance history so that copies never import unrelated decisions. Integration instructions are read from this README when needed, and target projects activate the protocol by inlining it into their own `AGENTS.md`.

Keep review reports and maintenance artifacts outside the copyable template tree, and do not copy them into target projects.
