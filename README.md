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
- **Progress is history:** It preserves confirmed conclusions, reasoning, rejected alternatives, and later amendments.
- **Living documents are snapshots:** They describe the rules currently in effect; they do not replace decision history.
- **The status index is navigation:** It helps locate records and understand their state without duplicating their full contents.

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

Record it informally in `Drafts/`, then discuss it with an agent or project collaborator. Different topics in one file may be confirmed separately. Leave unconfirmed topics pending. Once a conclusion is clear, archive it in `Progress/` and update the index.

### When an idea starts in conversation

A draft is not required. After a clear conclusion emerges, the agent should proactively archive it, preserve the original motivation in a “Discussion Origin” section, and mark the index source as “No corresponding draft; raised directly in conversation.” Never backdate or fabricate a draft to make the workflow appear complete.

### When a conclusion changes

Create a new record explaining which earlier decision is amended and why. Update the current living documents and, where useful, the old record's index status. Do not silently rewrite history so that the earlier conclusion appears never to have existed.

### After routine reviews or tests

If no reusable rule or new consensus emerged, do not create a Progress record. Existing test output, review logs, and commit history are sufficient. The workflow should reduce lost knowledge, not generate ceremonial documentation.

## Maintenance and Evolution

- The first version is plain text: no installer, initialization script, synchronization process, or runtime dependency.
- Projects may adapt copied templates to local needs. Copies are not automatically synchronized across projects.
- The generic protocol describes only the knowledge workflow. Coding, testing, release, and business rules remain in each project's own `AGENTS.md`.
- CLI tooling, version checks, and automatic synchronization should be considered only when real use in actual projects reveals a concrete need. They are not assumed to be inevitable next steps.

## Using This Kit to Maintain Itself

This directory is designed to be moved into a standalone repository. Once maintained independently, that repository may add its own root `AGENTS.md` referencing `AGENTS.knowledge.md`, allowing the kit to use the same workflow for its own evolution. This is optional and is not a required step when integrating the kit into another project.
