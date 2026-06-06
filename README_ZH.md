# CodexForGodot

> 独立开发者的 AI 全链路游戏开发框架。从构思到上架，一个人 + Codex 做完一款商品级游戏。

基于 [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) 深度改造。Codex 专属，Godot 专精。

[English](README.md) · [快速开始](#5-分钟上手)

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License"></a>
  <a href="https://godotengine.org/"><img src="https://img.shields.io/badge/Godot-4.x-478cbf" alt="Godot"></a>
  <a href="https://openai.com/index/codex/"><img src="https://img.shields.io/badge/Codex-required-412991" alt="Codex"></a>
  <a href="UPGRADING.md"><img src="https://img.shields.io/badge/from-CCGS%2021K%20%E2%98%85-informational" alt="Evolved from CCGS 21K Stars"></a>
  <img src="https://img.shields.io/badge/pipeline-%E6%9E%84%E6%80%9D%20%E2%86%92%20%E4%B8%8A%E6%9E%B6-brightgreen" alt="Full Pipeline: Concept to Ship">
</p>

<p align="center">
  <img src="demo-v5.gif" alt="从0开始，30分钟测试 Demo — Codex + Godot 实时演示" width="100%">
  <br>
  <em>从0开始，30 分钟做完的测试 Demo — Codex 实时驱动 Godot 开发</em>
</p>

---

## 为什么做这个

独立开发者做游戏，最大的问题不是缺想法——是缺人。程序你写，美术你画，数值你调，音效你找，测试你测，文案你写。每个环节都不够专业，每个环节都是你自己硬上。

AI 工具出现后，很多人尝试让 AI 帮忙写代码。但写代码只是游戏开发的一小部分。美术方向谁定？系统设计谁做？QA 谁跑？发布清单谁管？大多数 AI 工具只能帮你做游戏里的一小块——做个 Demo 还行，做完一整个商品级游戏？不行。

CodexForGodot 的目标：**一个人 + Codex，做完一款商品级品质的游戏。** 不是 Demo，不是原型——是能上架的游戏。

怎么做到？Codex 的多模态能力不只是写代码——它能生成和处理美术资源、理解设计文档、执行测试流程、编排发布清单。49 个 Agent 覆盖游戏开发所有职能：程序、美术、音频、文案、数值、关卡、QA、发布。17 个核心 Skill 从构思串到上架。你不再是孤军奋战的独狼，你是一个全 AI 团队的创意总监。

<details>
<summary><strong>和 CCGS 原版的关系</strong></summary>

CodexForGodot 从 [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios)（21K Stars）深度改造而来。CCGS 是很好的基础——49 Agent 的工作室架构、协作协议、设计流程都来自它。

这个 fork 做了这些具体的事：

- **砍掉无效确认** — 报告直接落盘，Lane 接手自动注册。砍掉的是"能写这个文件吗"这种零设计价值的确认。减少无意义环节,加速开发效率。
- **73 个命令合并为 17 个** — CCGS 的命令太多，环节太多，选择太多。我们合并同类项，旧名通过路由索引自动跳转。覆盖不减，上手更快。
- **多窗口 Lane 系统** — 每个职责（制作/开发/美术/QA/维护）跑在独立窗口，各自状态文件。并行不串扰。
- **技能融入思考** — `/skill-create-ccgs` 不直接塞命令，会判断：该不该存在？合并还是新建？
- **Codex 原生** — 框架需要 Codex 的机制才能运行，发挥 Codex 多模态和资源生成能力。我们希望 CODEX 能够替你完成一个完整的游戏,而不只是帮你写代码。
- **Godot 专精** — 不是多引擎模板选 Godot，是从 Agent 到 Skill 全部围绕 Godot 4.x + GDScript 打造。我们会提供更多的调试工具/资源制作方案。

变更细节见 [OPS-CHANGELOG.md](OPS-CHANGELOG.md)。

</details>

---

## 全链路覆盖

一个人做游戏，每个环节都要覆盖。CodexForGodot 把游戏开发拆成职能轨道，每个轨道有专门的 Agent 和 Skill：

```
构思 ──→ 设计 ──→ 开发 ──→ 测试 ──→ 发布
 │         │        │        │        │
brainstorm  design   dev-story  smoke   release
art-bible   system   story-done  bug    checklist
            arch     code-review  gate
```

| 职能 | Agent 覆盖 | Skill |
|------|-----------|-------|
| **构思** | 创意总监、游戏设计师 | `/brainstorm` — 概念、支柱、循环、原型方向 |
| **系统设计** | 系统设计师、数值设计师 | `/design-system` — GDD、设计审查、平衡校验 |
| **美术** | 美术总监、技术美术 | `/art-bible` — 视觉设定、资源规格、UX 规格 |
| **架构** | 技术总监、主程 | `/create-architecture` — 架构文档、ADR |
| **开发** | 各领域程序员 | `/dev-story` `/story-done` — 故事实现、验收 |
| **QA** | QA 负责人、测试员 | `/smoke-check` `/bug-report` `/gate-check` |
| **发布** | 发布经理 | `/release-checklist` — 发布清单、变更日志 |
| **框架** | 平台工程师 | `/skill-create-ccgs` `/setup-engine` |
| **导航** | 制作人 | `/start` `/help` `/window-ccgs` |

Codex 的多模态能力在这里发挥作用——不只是帮你写 GDScript，还能处理美术资源、生成设计素材、分析截图反馈。

---

## 和原版 CCGS 对比

| 维度 | CCGS | CodexForGodot |
|------|------|---------------|
| **目标** | AI 辅助游戏开发 | **一个人做完商品级游戏** |
| **AI 平台** | Claude Code | **Codex（需要 Codex 机制，利用多模态能力）** |
| **引擎** | 多引擎模板（Godot/Unity/UE） | **仅 Godot 4.x + GDScript** |
| **Skills** | 73 个命令 | **17 核心**（合并同类项，旧名自动跳转） |
| **多窗口** | 单窗口 | **多窗口并行 Lane，各自独立状态** |
| **无效确认** | 较多写入确认 | **报告自动落盘，Lane 自动注册** |
| **Skill 加入** | 直接添加 | **融入判断（该不该存在？合并还是新建？）** |

---

## 5 分钟上手

```bash
git clone https://github.com/ailess-lab/CodexForGodot.git my-game-studio
cd my-game-studio
codex
```

第一次启动：

```
/start
```

**试试看——真实的会话长这样：**

```
你: /brainstorm
Codex: 来设计你的游戏。先聊核心——你想让玩家在最初的 30 秒感受到什么？
你: 孤独的探索感，像废墟城市里的最后一个人。
     类似 Hollow Knight 遇上 Celeste 的移动手感。
Codex: 好锚点。我来探三个方向……

       [深度设计访谈]

       完整概念包：核心循环图 / 3 个支柱 / 原型范围 / 风险清单
       方向对吗？
你: 继续。

Codex: [设计方案落地为系统 GDD、架构文档、冲刺计划]

你: /window-ccgs B
Codex: [开发 Lane 启动，独立窗口，从状态文件恢复]
你: /window-ccgs C
Codex: [美术 Lane 启动，Codex 基于视觉设定处理美术资源]

       ……程序在 B 窗口写代码，美术在 C 窗口出资源，你在 A 窗口统筹方向。
```

---

## 多窗口 Lane 系统

独立开发者最大的痛点：所有事都在一个脑子里，所有任务都串在一个上下文里。程序还没写完，想起美术还没定方向。美术刚有想法，发现系统设计还没对齐。

多窗口 Lane 把这些职责拆到独立窗口：

| Lane | 职责 | 做什么 |
|------|------|--------|
| A | **制作** | 范围、优先级、跨窗口协调 |
| B | **开发** | 实现、Story、测试 |
| C | **美术** | 视觉方向、资源规格 |
| D | **QA** | 缺陷、冒烟测试、发布就绪 |
| Z | **平台** | Skills、Hooks、路由索引 |

每个窗口独立状态文件。关掉明天再开，`/window-ccgs B` 恢复。支持自定义：`/window-ccgs ui-polish`

---

## 从 CCGS 迁移

已在用 CCGS？参见 [UPGRADING.md](UPGRADING.md) 了解迁移方案。主要变化：
- Skill 名变了——旧名通过路由索引自动跳转
- `.claude/` → `.codex/` 目录结构
- `CLAUDE.md` → `AGENTS.md` 配置

---

## 许可

MIT License — 从 [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) 改造而来。
