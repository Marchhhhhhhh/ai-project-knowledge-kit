# Project Knowledge Kit

A **code-free, dependency-free** knowledge workflow for software projects. It separates raw ideas, confirmed decisions, decision history, and current project consensus so that contributors and AI agents can understand not only what was decided, but also why.

> **Core idea:** Preserve project memory in plain text, and use `AGENTS.md` to instruct agents how to maintain that memory.

## 中文介绍

这是一套从 Work Bench 抽离的**项目知识沉淀模板包**，用于在其他项目中复用 `Drafts/`、`Progress/`、归档规则和 `AGENTS.md` 组成的工作流。

- **Drafts（草稿箱）**：保留讨论前的真实想法，允许零碎、不成熟和一文多话题。
- **Progress（决策记录）**：保存已经确认的结论、理由、否决项和后续修订关系。
- **Progress.md（状态索引）**：帮助查找记录并判断处理状态，不重复完整论证。
- **AGENTS.knowledge.md（通用协议）**：由 Agent 合并进目标项目的 `AGENTS.md`，指导后续知识维护。
- **当前共识文档**：由目标项目指定，可以是已有 README、架构文档或产品文档，不强制新建。

模板包没有代码和运行时依赖，也不包含 Work Bench 的业务规则、真实草稿或历史决策。接入时必须保留目标项目已有内容，只创建缺失结构并合并协议，不能覆盖整个 `AGENTS.md` 或重写项目文档。

本模板包以英文为主体；本节仅作中文简介，完整的接入步骤、Agent 提示词和日常使用规则见下文。

## Directory Contents

```text
project-knowledge-kit/
├── README.md                 # This guide, including the Chinese introduction
├── AGENTS.knowledge.md       # Generic protocol to merge into a project's AGENTS.md
├── Drafts/
│   └── README.md             # Draft inbox guidance; optional after onboarding
└── Progress/
    ├── Progress.md           # Empty status index
    └── TEMPLATE.md           # Reference template for a decision record
```

The kit contains no project-specific decisions, business rules, or personal information. Once copied into a project, its knowledge records evolve independently within that project.

## Workflow Overview

```text
Raw ideas in Drafts/ ──discussion──> confirmed conclusions ──archive──> Progress/
                                             │
                                             └──update──> Progress/Progress.md

Ideas raised directly in conversation ──discussion──> confirmed conclusions
                                             │
                                             └──archive proactively; do not invent Drafts

Conclusions that affect current rules ──sync──> the project's designated living documents
                                               (README, architecture docs, AGENTS.md, etc.)
```

- **Drafts are inputs:** They may be incomplete, uncertain, or contain several topics. A draft is not a commitment to implement anything.
- **Archiving creates; it does not move:** After the user or another accountable human decision-maker explicitly accepts a conclusion, create a new decision record in `Progress/`, preserve the original draft and any unconfirmed topics, and update `Progress/Progress.md`. An agent's proposal or summary alone is not confirmation.
- **The index includes pending topics:** Add a new draft topic with `—` in the Record column and “Pending discussion” as its status. Replace the marker only when a confirmed decision has been archived.
- **Progress is history:** It preserves confirmed conclusions, reasoning, rejected alternatives, and later amendments.
- **Living documents distinguish now from later:** They describe current behavior separately from approved but unimplemented decisions; they do not replace decision history.
- **The status index is navigation:** It helps locate drafts and records and understand their state without duplicating their full contents.

## Agent Integration in Another Project

Give the following request to an agent working in the target project, together with this repository's URL or local path:

> Read `README.md` and `AGENTS.knowledge.md` in the Project Knowledge Kit repository, and integrate this code-free knowledge workflow into the current project. Create only missing `Drafts/` and `Progress/` structures and an empty index. Merge the generic protocol into the root `AGENTS.md` without overwriting existing content. Check for an existing knowledge or decision-recording workflow first, and surface any conflicts. Identify the project's living documents for current consensus. Do not copy illustrative examples as real project history or invent business decisions merely to populate the archive. When finished, report what was added, merged, preserved, and any conflicts that require human judgment.

The integrating agent should follow these steps:

1. **Inspect the target project**
   - Read its existing `AGENTS.md`, README, contribution guides, and other agent instructions.
   - Check for existing `Drafts/`, `Progress/`, decision records, or archiving rules. Preserve and reconcile existing content rather than replacing entire directories.
2. **Copy only the blank structure**
   - Create `Drafts/` and `Progress/` only when missing.
   - Use the kit's empty `Progress/Progress.md` and its `TEMPLATE.md`.
   - Do not copy real drafts, decisions, or images produced by this kit's use in any other project.
3. **Merge the protocol**
   - Merge `AGENTS.knowledge.md` into the target project's root `AGENTS.md`.
   - Preserve all unrelated project-specific rules. Do not delete or rewrite them merely to make the text look uniform.
   - If the project uses additional agent-instruction files, follow its existing convention for referencing the root `AGENTS.md` instead of creating several independently maintained copies.
4. **Identify living documents**
   - Prefer existing README, architecture, product, or other current-consensus documents.
   - Do not require a new README or rewrite the project's design philosophy just to adopt this workflow.
5. **Perform lightweight verification**
   - Confirm that the new index contains no invented drafts or decisions.
   - Confirm that the merged protocol covers startup draft checks, archiving confirmed conclusions, proactive archiving of direct conversations, partial-topic handling, amendment history, living-document synchronization, and noise control.
   - Report all file changes and any rule conflicts that need human resolution.

## Day-to-Day Use

### When an idea starts as a draft

Record it informally in `Drafts/`, and add each topic to `Progress/Progress.md` with `—` in the Record column and “Pending discussion” as its status. Discuss it with an agent or project collaborator. Different topics in one file may be confirmed separately.

“Confirmed” means that the user or another accountable human decision-maker has explicitly accepted a specific conclusion or option. An agent's proposal, summary, or interpretation of silence is not confirmation. If the accepted scope is unclear, ask before archiving.

Once a conclusion is confirmed, archiving consists of three actions: **create a new decision record in `Progress/`, preserve the original draft and its unconfirmed topics, and update the index**. Do not move or delete the original draft. Keep unconfirmed topics in separate pending rows; create a separate row for each archived decision.

### When an idea starts in conversation

A draft is not required. After a human-confirmed conclusion emerges, the agent should proactively archive it without asking again for permission to perform the record-keeping step. Preserve the original motivation in a “Discussion Origin” section, and mark the index source as “No corresponding draft; raised directly in conversation.” Never backdate or fabricate a draft to make the workflow appear complete.

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

Immediately index both undiscussed topics in `Progress/Progress.md`. There are no conclusions or decision records yet:

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/20261117_01.md (Export format) | — | Pending discussion | 2026-11-17 | JSON and CSV support not yet decided |
| Drafts/20261117_01.md (Notification timing) | — | Pending discussion | 2026-11-17 | Timing not yet decided |

### 2. Confirm and archive only the first topic

During discussion, an agent recommends supporting JSON first and postponing CSV. That recommendation alone is not confirmation. The user then explicitly replies, “Yes, use JSON only for the first version; CSV remains undecided.” The export-format topic is now confirmed within that specific scope.

Create `Progress/20261117_01-json-export.md`:

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

The original draft remains unchanged, including both topics. Update the index so the first topic points to its new record and the second remains pending:

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/20261117_01.md (Export format) | Progress/20261117_01-json-export.md | Confirmed, pending implementation | 2026-11-18 | JSON only for the first version; CSV remains undecided |
| Drafts/20261117_01.md (Notification timing) | — | Pending discussion | 2026-11-18 | Timing not yet decided |

If the README describes current application behavior, do not add “JSON export is available.” Instead, if advance documentation is useful, add a clearly separated section:

```markdown
## Approved, Not Yet Implemented

- JSON-only export has been approved for the first version.
  See `Progress/20261117_01-json-export.md`. It is not currently available.
```

### 3. Confirm the second topic independently

On a later date, the user explicitly chooses a daily digest for notifications. Create a second record, `Progress/20261118_01-daily-digest.md`, while preserving the same original draft. The index now contains two separate decision records and no pending rows for this draft:

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/20261117_01.md (Export format) | Progress/20261117_01-json-export.md | Confirmed, pending implementation | 2026-11-18 | JSON only for the first version; CSV remains undecided |
| Drafts/20261117_01.md (Notification timing) | Progress/20261118_01-daily-digest.md | Confirmed, pending implementation | 2026-11-19 | Send a daily digest; immediate notifications not approved |

Confirming the second topic does not rewrite the first record or imply that either feature has been implemented.

### 4. Amend the export decision without erasing history

After implementation has begun, a real integration requirement makes CSV necessary. The agent does not silently change the old conclusion. It presents the new trade-off, and the user explicitly approves JSON and CSV together.

Create a new record, `Progress/20261120_01-json-and-csv-export.md`, stating that it amends `Progress/20261117_01-json-export.md` and why. Update the living document to describe JSON and CSV as approved future behavior until both are implemented and verified. The index retains both records:

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/20261117_01.md (Export format) | Progress/20261117_01-json-export.md | Amended by a later decision | 2026-11-20 | JSON-only scope amended by 20261120_01-json-and-csv-export.md |
| Drafts/20261117_01.md (Export format) | Progress/20261120_01-json-and-csv-export.md | Confirmed, pending implementation | 2026-11-20 | JSON and CSV approved; supersedes the earlier format scope |
| Drafts/20261117_01.md (Notification timing) | Progress/20261118_01-daily-digest.md | Confirmed, pending implementation | 2026-11-19 | Send a daily digest; immediate notifications not approved |

The original draft and both export records remain available. The old record shows what was approved at that time, the new record shows the current approved direction, and the README continues to distinguish approved future behavior from verified existing behavior.

## Maintenance and Evolution

- The first version is plain text: no installer, initialization script, synchronization process, or runtime dependency.
- Projects may adapt copied templates to local needs. Copies are not automatically synchronized across projects.
- The generic protocol describes only the knowledge workflow. Coding, testing, release, and business rules remain in each project's own `AGENTS.md`.
- CLI tooling, version checks, and automatic synchronization should be considered only when real use in actual projects reveals a concrete need. They are not assumed to be inevitable next steps.

## Using This Kit to Maintain Itself

This repository is maintained independently. It may add its own root `AGENTS.md` referencing `AGENTS.knowledge.md`, allowing the kit to use the same workflow for its own evolution. This is optional and is not a required step when integrating the kit into another project.
