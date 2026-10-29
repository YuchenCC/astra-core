# Astra Core · 星枢：贡献者协作说明书

Astra Core 是以人力为首个领域的业务 AI 场景运行框架。本工程当前的交付目标是形成一份可供 AI 原生研发使用的需求范围与技术架构设计说明书，尚无业务代码、构建工程或运行 Demo。

仓库：[YuchenCC/astra-core](https://github.com/YuchenCC/astra-core)。开发与文档修订统一使用 Codex；人负责业务取舍和最终确认。

## 先理解这三类材料

| 材料 | 用途 | 是否构成业务依据 |
| --- | --- | --- |
| [唯一说明书](docs/baseline/specification.md) | 需求、架构、决策、验收和未决项 | main 上明确确认的内容是基线；分支版本是候选稿 |
| [当前 Handoff](docs/handoff/current.md) | 进度、下一步、阻塞和任务指导 | 不新增或覆盖需求结论 |
| 本任务纪要与提案 | 记录本次输入、取舍、建议与确认 | 解释修订来源，不能自动当作已确认需求 |

main 是唯一主线，仍可含明确标注的待确认项。“合并”不表示所有业务问题已解决。当前 M1 仅场景定义与管理需求完成，下一业务专题是 M2。

```text
README.md                         人的协作入口
AGENTS.md                         Codex 的执行规则
.agents/skills/                    提交 PR / 整合合并 PR
  astra-submit-pr/
  astra-merge-pr/
docs/
  baseline/specification.md        唯一业务说明书
  handoff/current.md                项目当前交接
collaboration/
  templates/                      任务 Handoff、纪要、提案模板
  tasks/<task-id>/                 本任务的过程与交接
archive/pre-collaboration/         历史快照，默认不读
```

## 协作前准备

1. 确认 GitHub 仓库写入权限；检查 SSH 或 HTTPS 凭证。只读访问公开仓库不代表可以 push。
2. 在本地 clone 仓库并配置自己的 Git 作者身份。不要复用他人的作者身份或提交凭证到仓库。
3. 使用 Codex 打开本任务的独立工作目录。每个新任务开启新会话，并行任务使用不同 checkout 或 worktree。
4. 先读本页、[AGENTS.md](AGENTS.md)、唯一说明书和当前 Handoff，再确定专题、负责人和完成标准。

新建工作目录的示例（将尖括号内容替换为实际值）：

```sh
git clone git@github.com:YuchenCC/astra-core.git
cd astra-core
git config user.name '<你的名字>'
git config user.email '<你的提交邮箱>'
git fetch origin
git switch -c docs/<owner>/<topic> origin/main
```

同一 clone 并行处理另一任务时，可让 Codex 创建独立 worktree，并在其目录开启新会话。不要在其他协作者正在使用的目录切换分支。

## 第一次参与：给 Codex 一个明确任务

任务标识使用 `<owner>-<topic>` 等唯一名字；一次分支围绕一个专题，不长期累积多个无关议题。可使用 GitHub Issue 协调范围，但不要求先创建 Issue。

可复制的开场：

> 请按 AGENTS.md 开始新任务 `<task-id>`，负责人为 `<owner>`，范围是 `<专题与完成标准>`。先读取当前唯一说明书和项目 Handoff，从最新 origin/main 建立工作分支，并基于 collaboration/templates 创建本任务材料。记录实际来源提交；不要读取历史归档、其他任务的纪要或过程稿。先讨论未确认的业务取舍，经我确认后再修改候选说明书。

Codex 在本任务目录维护 [Handoff 模板](collaboration/templates/handoff.md)、[纪要模板](collaboration/templates/notes.md)和[提案模板](collaboration/templates/proposal.md)。普通收尾更新本任务 Handoff，影响项目进度或准备合并时才同步项目 Handoff。

## 日常修订与上下文隔离

讨论形成建议，人的明确确认支持落稿；正文在工作分支里仍然是候选稿。纪要记录问题、关键事实、取舍及确认依据，不必复制完整聊天，不记录凭证或个人业务数据。

新任务仅从当前基线及 Handoff 建立上下文。不要让 Codex 为“了解项目”扫描全部 Markdown，或重新解释其他同学的聊天。确需追溯时，由人指定材料范围；合并指定 PR 时可定向读取该 PR 的修订记录。

AGENTS.md 不能清除旧会话已有内容；分支也不能隔离同一个聊天的记忆。因此换专题要换会话，任务并行要换目录。断点续接则使用原任务 Handoff，读取该任务纪要仍需明确指定。

重大变更完成检查后，Codex 自动提交并推送工作分支。main 不直接写入，推送不等于合并或业务批准。

## 提交与合并：使用两个共享 Skill

Skill 随仓库位于 `.agents/skills`，无需安装个人副本；客户端未发现时，直接指定读取 SKILL.md。操作细节以相应 Skill 为准。

| 操作 | 调用示例 | 结果 |
| --- | --- | --- |
| 提交修订 | `使用 $astra-submit-pr，为任务 <task-id> 提交或更新 PR。` | 工作分支已提交上传，PR 附标准修订说明，等待审阅 |
| 整合并准备合并 | `使用 $astra-merge-pr 整合 PR #<编号>，生成完整候选说明书供我确认。` | 基于新旧文档及记录重整全文，提交后等待人工确认 |
| 最终合并 | `我确认 PR #<编号> 的 head <SHA>，基于 main <SHA> 的最终整合结果，请合并。` | 核对版本及实际权限/规则后合并并验证 |

未发现 Skill 时的替代说法：

> 请读取 `.agents/skills/astra-submit-pr/SKILL.md`，按其流程提交任务 `<task-id>`。

提交 Skill 见[提交规范](.agents/skills/astra-submit-pr/SKILL.md)，整合 Skill 见[整合规范](.agents/skills/astra-merge-pr/SKILL.md)。PR 统一使用[标准修订说明](.agents/skills/astra-submit-pr/references/pr-template.md)，包含来源提交、前后结论、理由、确认状态、影响、纪要、检查和人工判断事项。

流程：专题分支讨论和修订 → 提交 PR → AI 对照最新 main 和修订记录整合 → 在 PR 中提交完整新说明书 → 人确认最终版本 → 合并 main。旧文档由 Git 保留，固定路径只维护一份当前说明书。

AI 可以整理结构、统一术语和修复引用；业务取舍或语义冲突必须明确提出，不自行折中。人工确认需覆盖最终候选提交和最新主线，确认后又有实质修改或 main 前进，需要重新检查确认。首期仓库所有者作为最终确认人，任务可另指定业务与架构审阅人；贡献者不能仅凭自己的提交说明视作批准。

## 遇到这些情况怎么办

| 情况 | 处理 |
| --- | --- |
| 继续原任务 | 指定任务标识，读取本任务 Handoff；查看工作区和实际 Git 状态后续接 |
| 开启新任务 | 新会话、从最新 main 开短期分支，不加载旧纪要 |
| main 已更新 | 比较本任务起点、最新 main 与候选稿；无 Git 冲突也要检查业务语义 |
| 两份文档结论矛盾 | 列出冲突与影响，由人判断；不按修改时间或纪要自动取舍 |
| push 失败 | 保留本地提交、记录失败和恢复方法；可通过已授权连接器发布并核对，仍要披露命令行限制 |
| 需要了解历史理由 | 人明确指定旧材料范围；历史记录仅作参考，不能覆盖有效基线 |
| 新增需求或废止旧项 | 保持编号稳定，不复用；记录依据、状态和替代关系 |

## 三份简短清单

协作前：任务范围和负责人明确；会话/目录独立；知道来源 main 提交及允许读取材料。

提交前：正文、纪要和交接一致；区分建议与确认；检查链接、编号、差异及实际上传结果；PR 修订说明完整。

确认合并前：看的是最终完整说明书；取舍已经明确；没有丢失既有约束；确认覆盖当前 head 与 main，之后的修改未绕过审阅。

本工程不提供检查脚本或 GitHub Actions；检查由 Skill 指导 Codex 执行并报告。GitHub 在线分支保护不在本次改造中配置，文本规范不等于服务端限制；后续建议要求 PR、人工审批、修改后重新审批并禁止直接推送 main。
