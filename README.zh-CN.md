# 项目知识沉淀模板包

[English](README.md) | **简体中文**

**让你的草稿与 Agent 对话中的见解，汇入一套共享、可追溯的项目记忆。**

随时写下想法，或者直接开始讨论。两条路径最终汇入同一套决策历史——既不必把即时对话硬写成草稿，也不会让有价值的结论消失在聊天记录里。

```text
你的草稿                              Agent 对话
想法、问题、背景                      见解、提案、澄清
        │                                     │
        └───────────────┬─────────────────────┘
                        ▼
                  人工确认的决策
                        │
                        ▼
              可追溯历史 + 当前共识
```

Agent 负责整理和归档；有决策权的人负责确认。两条路径是同一知识工作流的平等入口，而非彼此竞争的工作方式。

这是一套面向软件项目的**无代码、无运行时依赖**方案，只使用纯文本和 `AGENTS.md`。它分离原始想法、已确认决策、决策历史和当前项目共识，让贡献者和 AI Agent 不仅知道决定了什么，也知道为什么这样决定。

当前分发版本：**0.2.0**（见 [VERSION](VERSION)）。通过 Git 接入时记录完整的源提交 SHA；通过 ZIP 或复制目录接入时记录来源位置及此版本。

## 目录内容

```text
ai-project-knowledge-kit/
├── README.md                 # 英文指南
├── README.zh-CN.md           # 本指南的中文翻译
├── AGENTS.knowledge.md       # 合并到目标项目 AGENTS.md 的通用协议
├── VERSION                   # 用于非 Git 接入和升级的分发版本
├── LICENSE                   # 允许复用和改编的 MIT 许可证
├── .gitignore                # 最小化的操作系统文件排除规则
├── Drafts/
│   └── README.md             # 草稿箱指南；默认复制，冗余时可删除
└── Progress/
    ├── Progress.md           # 不含真实项目记录的索引模板
    └── TEMPLATE.md           # 决策记录参考模板
```

模板文件不包含特定项目的决策、业务规则或个人信息。复制到项目后，其中的知识记录会在该项目内独立演化。

本模板包以 [MIT 许可证](LICENSE)分发。目录树标明默认模板内容；接入时只复制下文明确列出的文件。评审报告、维护笔记及其他仓库维护产物不属于项目模板。

## 术语

- **当前共识文档（Living documents）**是由项目指定、描述当前生效共识的文档，例如 README 或架构文档。“当前项目共识”是这些文档传达的内容，不是另一个独立存储位置。
- **决策记录（Decision records）**是 `Progress/` 中按日期组织的文件，用于保存结论及其上下文。
- **状态索引（Status index）**是 `Progress/Progress.md`，不是整个 `Progress/` 目录。

## 工作流概览

```text
Drafts/ 中的原始想法 ──讨论──> 已确认结论 ──归档──> Progress/
                                      │
                                      └──更新──> Progress/Progress.md

对话中直接提出的想法 ──讨论──> 已确认结论
                                      │
                                      └──归档──> Progress/

影响当前规则的结论 ──同步──> 项目指定的当前共识文档
                            （README、架构文档、AGENTS.md 等）
```

对于直接对话中的结论，经人工确认后应主动归档，不得虚构草稿。

- **草稿是输入：**草稿可以不完整、不成熟，也可以包含多个话题。草稿不代表必须实施的承诺。
- **归档是新建，不是移动：**用户或其他对项目决策负责的人明确接受结论后，在 `Progress/` 中新建决策记录，保留原始草稿及其未确认话题，并更新 `Progress/Progress.md`。Agent 的提案或总结本身不构成确认。
- **索引包含待处理话题：**新增草稿话题时，在 Record 列填写 `—`，状态填写 `Pending discussion`。只有已确认的决策完成归档后，才用记录路径替换该标记。
- **Progress 保存历史：**它保存已确认结论，包括拒绝和暂缓决定、理由、被否决的备选方案及后续修订。
- **待处理话题有退出机制：**人工决定不实施或暂缓时，应归档并关联记录，状态分别使用 `Rejected` 或 `Deferred`，而不是永远保持待处理。
- **当前共识文档区分现在与未来：**它们分别描述当前行为和已批准但尚未实现的决策，不能替代决策历史。
- **状态索引用于导航：**它帮助定位草稿和记录并了解状态，无需复制完整内容。

## 在其他项目中由 Agent 接入

将以下请求与本仓库的 URL 或本地路径一起交给目标项目中的 Agent：

> Read `README.md` and `AGENTS.knowledge.md` in the Project Knowledge Kit repository, and integrate this code-free knowledge workflow into the current project. Create only missing `Drafts/` and `Progress/` structures, including `Progress/TEMPLATE.md` and `Progress/Progress.md` with its header rules but no real project records; copy `Drafts/README.md` unless the project already covers its rules and deliberately retains the draft directory another way. Remove the illustrative comments from the copied index. Inline the generic protocol into the root `AGENTS.md` without overwriting existing content, recording the source repository URL or distribution location and the exact source commit SHA or distribution version immediately above the merged protocol. Then remove only the standalone `AGENTS.knowledge.md` copy introduced by this integration; preserve any pre-existing file with that name. Check for an existing knowledge or decision-recording workflow first, and surface any conflicts. Identify the project's living documents for current consensus. Copy only the template files listed in the integration steps, not maintenance artifacts such as `Docs/`. Do not copy illustrative examples as real project history or invent business decisions merely to populate the archive. When finished, report what was added, merged, preserved, the recorded protocol version, and any conflicts that require human judgment.

负责接入的 Agent 应遵循以下步骤：

1. **检查目标项目**
   - 阅读已有的 `AGENTS.md`、README、贡献指南及其他 Agent 指令。
   - 检查已有的 `Drafts/`、`Progress/`、决策记录或归档规则。保留并协调已有内容，不要替换整个目录。
2. **只复制空白模板结构**
   - 仅在缺失时创建 `Drafts/` 和 `Progress/`。
   - 复制 `Drafts/README.md`、`Progress/Progress.md` 和 `Progress/TEMPLATE.md`。默认保留草稿指南，因为 Git 不跟踪空目录，而且该指南说明了待处理话题索引和草稿保留规则。只有合并后的 `AGENTS.md` 已覆盖这些规则，且项目另有明确方式保留 `Drafts/` 时，才可以省略。
   - 复制带有表头规则且不含真实项目记录的 `Progress/Progress.md`。删除说明性 HTML 注释，但保留表格及其说明。
   - 不复制本模板包在其他项目中使用时产生的真实草稿、决策或图片，也不复制 `Docs/` 等仓库维护产物。
3. **内联协议，作为唯一维护副本**
   - 将 `AGENTS.knowledge.md` 的内容合并到目标项目根目录的 `AGENTS.md`。本仓库的 `.knowledge` 后缀只是接入前的暂存约定，并不是多数 Agent 会自动发现的文件名。
   - 在合并后的协议正上方添加来源注释，标明实际使用的来源。Git 来源使用仓库 URL 和完整提交 SHA：`<!-- Project Knowledge Protocol source: https://github.com/OWNER/ai-project-knowledge-kit @ FULL_COMMIT_SHA -->`。ZIP 或复制目录来源使用其位置和 `VERSION` 中的版本：`<!-- Project Knowledge Protocol source: DISTRIBUTION_LOCATION @ version 0.2.0 -->`。将所有占位符替换为实际来源信息，不要记录未指定版本的分支名。后续升级时保留此定位注释。
   - 成功内联合并后，只删除本次接入引入的独立 `AGENTS.knowledge.md` 副本。保留此前已有的同名文件，直到用户明确其用途。不要同时保留可能漂移的内联副本和引用副本。
   - 保留所有无关的项目专属规则，不要仅为统一文本风格而删除或改写。
   - 如果项目使用其他 Agent 指令文件，遵循其引用根 `AGENTS.md` 的既有约定，不要创建多份独立维护的副本。
   - 已集中管理 Agent 指令的项目，只有在其 Agent 运行环境确实会遵循外部引用，且项目明确选择单一维护来源时，才可以保留外部引用而不内联。不要假设提及路径就会自动生效。
4. **确定当前共识文档**
   - 优先使用已有的 README、架构、产品或其他当前共识文档。
   - 不要为了采用此工作流而强制新建 README 或重写项目设计理念。
5. **执行轻量校验**
   - 确认新索引保留表头规则，且没有虚构草稿或决策。
   - 确认合并后的协议覆盖：按月及按作者命名草稿、稳定的带日期条目编号、精确的 Source 引用、Agent 在不改写真实输入的前提下补全元数据、旧草稿兼容性、讨论开始时检查草稿、由负责的人确认、待处理话题及未决子范围索引、归档的三个动作、主动归档直接对话、记录命名、拒绝及暂缓退出、后续重新开启、修订历史、区分当前行为与已批准的未来行为，以及噪声控制。
   - 确认状态值拼写完全一致，并且 `Drafts/README.md` 已存在，或其待处理话题索引、草稿保留和推荐的月度条目规则已由其他文档覆盖。
   - 确认合并后的协议带来源注释，其中包含实际来源位置，以及完整上游提交 SHA 或所用的 `VERSION` 值。
   - 报告所有文件变更及需要人工解决的规则冲突。

## 日常使用

### 想法从草稿开始

在 `Drafts/` 中随意记录，并将每个话题加入 `Progress/Progress.md`，Record 列填写 `—`，状态填写 `Pending discussion`。个人或低频协作时推荐文件名 `YYYYMM.md`；多人并行协作时使用 `YYYYMM_author.md`，其中作者标识为稳定的团队账号或作者 ID，以便贡献者分别向自己的文件追加内容。月文件内使用 `YYYY-MM-DD` 标题按日期分组，并在每个日期下使用 `01`、`02` 等编号及简短主题标题。日期指条目的实际收录日期，而非最初产生想法的日期。不要重新编号，也不要将未处理条目移到后续月份。同一文件中的不同话题可以分别确认。

保留作者原文。Agent 收录想法或收到不含推荐元数据的草稿时，应使用实际收录日期、追加当日下一个编号并添加简短标题，而不是要求作者重写。不得根据文件时间戳推断更早的想法日期。历史材料可以使用实际导入日期并注明导入，或注明原始日期未知。Source 引用应标明文件、条目日期、编号和话题范围。旧 `YYYYMMDD_sequence.md` 文件继续有效，无需改名。

“已确认”指用户或其他对项目决策负责的人明确接受了具体结论或选项。Agent 的提案、总结或对沉默的推断不算确认。如果已接受的范围不清楚，归档前应先询问。

结论确认后，归档由三个动作组成：**在 `Progress/` 中新建决策记录、保留原始草稿及其未确认话题、更新索引**。不要移动或删除原始草稿。未确认话题保留在单独的待处理行中，每项已归档决策也单独建立索引行。

同一话题中的未决问题也适用此规则。如果某项决策只确认了话题的一部分，应为每个剩余未决子范围建立待处理行，而不能只在已确认记录的 Notes 中提及。待处理子范围只有经人工明确决策才算解决，不会因父话题的决策而被隐式批准或拒绝。

### 想法从对话开始

不要求先有草稿。形成经人工明确确认的结论后，Agent 应主动归档，无需再次请求执行归档的许可。在“Discussion Origin”一节保留最初动机，并将索引来源标为 `No corresponding draft; raised directly in conversation`。不得为了让工作流看起来完整而倒填或虚构草稿。

### 想法被拒绝或暂缓

决定不实施或暂缓实施，也是能够让待处理事项退出的已确认结论。创建解释理由的决策记录，将话题的索引行关联到该记录，并准确使用状态 `Rejected` 或 `Deferred`。不要仅因不会实施就让该行保持 `Pending discussion`。

如果之后重新考虑并接受该话题，应为新确认的范围创建新记录和新索引行。将旧的 `Rejected` 或 `Deferred` 行改为 `Amended by a later decision`，在 Notes 中标明新记录，并保留旧记录的原始结论。这里复用已有的修订状态，不需要单独的 `Reopened` 状态。

### 结论发生变化

创建新记录，说明修订了哪项早期决策及原因。更新当前共识文档，并在有帮助时更新旧记录的索引状态。不得悄悄改写历史，让早期结论看似从未存在。

### 决策已批准但尚未实现

不要将计划行为描述为已经存在。如果实现前需要写入当前共识文档，应放在醒目的 `Approved, not yet implemented` 等标题下并链接决策记录。已有使用说明和当前行为描述保持不变。实现并验证后，将说明移至当前行为部分，移除待实现标签，并更新记录和索引状态。

### 例行评审或测试之后

如果没有产生可复用规则或新共识，无需创建 Progress 记录。保留原有测试输出、评审日志和提交历史即可。此工作流应减少知识丢失，而不是制造形式化文档。

## 完整虚构示例

以下示例完全虚构，用于说明文件关系和状态转换。它不是本仓库的真实决策，也不是应复制为项目历史的模板。

### 1. 记录两个话题，但不视为已批准

创建 `Drafts/202611_lqf.md`，在同一日期下写入两个条目：

```markdown
# November 2026 Drafts

## 2026-11-17

### 01 Export format

Could we support both JSON and CSV exports?

### 02 Notification timing

Should notifications be sent immediately or collected into a daily digest?
```

作者后缀让并行贡献者分别使用不同文件；个人或低频项目可以使用 `Drafts/202611.md`。决策记录文件名使用归档日期和当日记录序号，而非来源条目的日期或编号。Source 列建立草稿关联。以下各条记录有意使用不同日期。旧的按天草稿文件可以保留原名；只有新收录的条目需要遵循月度约定。

立即在 `Progress/Progress.md` 中登记两个尚未讨论的话题；此时还没有结论或决策记录：

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/202611_lqf.md (2026-11-17 / 01 / Export format) | — | Pending discussion | 2026-11-17 | JSON 和 CSV 支持尚未决定 |
| Drafts/202611_lqf.md (2026-11-17 / 02 / Notification timing) | — | Pending discussion | 2026-11-17 | 通知时机尚未决定 |

### 2. 只确认并归档 JSON 范围

讨论中，Agent 建议先支持 JSON、暂缓 CSV。该建议本身不是确认。随后用户明确回复：“是的，第一版只使用 JSON；CSV 仍未决定。”此时导出格式话题已在该具体范围内得到确认。

创建 `Progress/20261118_01-json-export.md`：

```markdown
# Decision Record: JSON Export for the First Version

- Source: `Drafts/202611_lqf.md` (2026-11-17 / 01 / Export format)
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

原始草稿保持不变，包括两个话题。更新索引，让已确认的 JSON 范围指向新记录。未来 CSV 支持成为 Export format 下单独的待处理子范围，不能只存在于已确认记录的 Notes 中。通知时机也仍然待处理：

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/202611_lqf.md (2026-11-17 / 01 / Export format — first-version JSON support) | Progress/20261118_01-json-export.md | Confirmed, pending implementation | 2026-11-18 | 第一版已批准使用 JSON |
| Drafts/202611_lqf.md (2026-11-17 / 01 / Export format — future CSV support) | — | Pending discussion | 2026-11-18 | 用户明确保留为未决定 |
| Drafts/202611_lqf.md (2026-11-17 / 02 / Notification timing) | — | Pending discussion | 2026-11-18 | 通知时机尚未决定 |

如果 README 描述的是当前应用行为，不要添加“JSON 导出已可用”。如果提前说明有用，应添加明确分隔的区块：

```markdown
## Approved, Not Yet Implemented

- JSON-only export has been approved for the first version.
  See `Progress/20261118_01-json-export.md`. It is not currently available.
```

### 3. 确认另一个话题，但不解决 CSV 子范围

之后某日，用户明确选择每日汇总通知。创建第二条记录 `Progress/20261119_01-daily-digest.md`，同时保留同一原始草稿。索引现在包含两条独立决策记录，但未来 CSV 支持仍待处理，因为通知决策没有涉及它：

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/202611_lqf.md (2026-11-17 / 01 / Export format — first-version JSON support) | Progress/20261118_01-json-export.md | Confirmed, pending implementation | 2026-11-18 | 第一版已批准使用 JSON |
| Drafts/202611_lqf.md (2026-11-17 / 01 / Export format — future CSV support) | — | Pending discussion | 2026-11-19 | 仍未决定；通知决策未解决此项 |
| Drafts/202611_lqf.md (2026-11-17 / 02 / Notification timing) | Progress/20261119_01-daily-digest.md | Confirmed, pending implementation | 2026-11-19 | 使用每日汇总；未批准即时通知 |

确认通知时机不会改写 JSON 记录、解决 CSV 子范围，也不表示任何已确认功能已经实现。

### 4. 解决 CSV 并修订导出决策，同时保留历史

实现开始后，真实的集成需求使 CSV 成为必需。Agent 不会悄悄改变旧结论，也不会假装 CSV 早已获批。它提出新的取舍，由用户明确批准同时支持 JSON 和 CSV。这既解决了待处理的 CSV 子范围，也修订了此前仅支持 JSON 的决策。

创建新记录 `Progress/20261120_01-json-and-csv-export.md`，说明它修订了 `Progress/20261118_01-json-export.md` 及原因。用新记录路径替换 CSV 待处理行中的 `—` 并更新状态。在两者均实现并验证前，将当前共识文档中的 JSON 和 CSV 描述为已批准的未来行为。索引保留旧决策、新决策和通知决策：

| Source | Record | Status | Updated | Notes |
|---|---|---|---|---|
| Drafts/202611_lqf.md (2026-11-17 / 01 / Export format — first-version JSON support) | Progress/20261118_01-json-export.md | Amended by a later decision | 2026-11-20 | 仅支持 JSON 的范围已由 20261120_01-json-and-csv-export.md 修订 |
| Drafts/202611_lqf.md (2026-11-17 / 01 / Export format — future CSV support) | Progress/20261120_01-json-and-csv-export.md | Confirmed, pending implementation | 2026-11-20 | CSV 已明确批准；JSON 和 CSV 共同构成已批准的导出范围 |
| Drafts/202611_lqf.md (2026-11-17 / 02 / Notification timing) | Progress/20261119_01-daily-digest.md | Confirmed, pending implementation | 2026-11-19 | 使用每日汇总；未批准即时通知 |

原始草稿和两条导出记录均保留。旧记录显示当时批准的内容，CSV 待处理行持续跟踪未决子范围直到明确解决，新记录显示当前批准方向。README 继续区分已批准的未来行为与已验证的现有行为。

## 维护与演进

- 首个版本采用纯文本：没有安装器、初始化脚本、同步过程或运行时依赖。
- 项目可根据本地需求调整复制后的模板。各项目中的副本不会自动同步。
- 每份内联协议都携带来源位置及准确的上游提交 SHA 或分发版本。Git 来源使用完整提交 SHA；ZIP 和复制目录来源使用 `VERSION` 中的值。升级时，比较已记录版本与目标上游版本并审查协议差异；报告对本地定制及现有工作流的影响；实质性变更需取得项目负责人确认；然后有意合并并更新来源版本。升级时不得覆盖整个 `AGENTS.md`。
- 发布变更后的分发版本时，在同一变更中更新 `VERSION` 及两份 README 译本中的对应版本引用。Git 标签可选；版本文件是非 Git 使用者的可移植依据。
- 通用协议只描述知识工作流。编码、测试、发布和业务规则仍由各项目自己的 `AGENTS.md` 管理。
- 只有在真实项目使用暴露出具体需求后，才考虑 CLI 工具、版本检查和自动同步。它们并非必然的下一步。

## 使用本模板包维护自身

本模板包仓库有意不设置根 `AGENTS.md`，也不在模板 `Progress/` 中维护真实项目决策记录。它是协议来源，不是业务项目；模板文件必须保持不含仓库维护历史，避免副本引入无关决策。需要时从本 README 读取接入说明，目标项目通过将协议内联到自己的 `AGENTS.md` 来启用它。

评审报告和维护产物应放在可复制模板树之外，不得复制到目标项目中。
