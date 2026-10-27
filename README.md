# Astra Core · 星枢

业务 AI 场景运行框架，以人力资源管理为首个领域。

协作基线 0.6 · 2026-10-27 · 文档工程，无可运行代码

以 Spring AI 为底座、FastAI 为外部模型能力，向原系统提供场景能力调用与托管对话。以人力为首个领域，通用底座可共享给其他业务系统。

## Codex 协作入口

本项目以 Codex 为唯一开发工具。新会话先读 [AGENTS.md](AGENTS.md)、[工作进度](docs/09-work-progress.md)，再按[协作与版本交接规范](docs/10-codex-workflow.md)推进。重大变更完成检查后，由 Codex 自动 commit 并 push；操作结果必须核实，失败保留本地提交并记录阻塞。

远程仓库：[YuchenCC/astra-core](https://github.com/YuchenCC/astra-core)，默认分支 `main`。

## 下次从这里继续

先读 [Handoff 与讨论路线](docs/06-discussion-roadmap.md)，再读 [架构设计说明书](docs/08-architecture-guide.md)。当前采用 M1—M7 七模块架构，下一轮从 **M2 执行与上下文** 的一次业务目标及对象关系开始。

**已完成的是 M1 的场景定义与管理需求**；M1 的具体接入协议与界面集成尚未完成。当前只做需求分析与文档，先讨论、确认后同步，不生成业务代码，不把提案写成已确认需求。

## 当前材料

| 文档 | 职责 |
| --- | --- |
| [接续说明](docs/06-discussion-roadmap.md) | 当前共识、七模块进度、下一轮问题和可复制开场 |
| [架构设计说明书](docs/08-architecture-guide.md) | 协作者串讲：定位、两端交互、七模块图、场景案例、代码组织建议 |
| [M1 场景定义与管理](docs/07-scene-requirements.md) | 已确认需求及 M1-REQ-001—031，含注册版本、契约、依赖与选择 |
| [需求范围](docs/01-requirements.md) | 项目事实、范围、非目标与质量需求 |
| [场景与 Demo](docs/02-scenarios.md) | 验证样例与尚未确认的 Demo 深度 |
| [架构基线](docs/03-architecture.md) | 核心概念、策略、边界及实现建议 |
| [当前决策与待定项](docs/04-feasibility-decisions.md) | 有效决策、外部依赖、风险及后续验证 |
| [七模块能力地图](docs/05-capability-map.md) | 模块职责、协作关系和进度 |

正文按当前基线维护，不依赖历史讨论编号。代码目录、Maven 拆分、接口协议、状态机、存储及框架版本仍按各专题确认；逻辑模块不等于工程或部署单元。
