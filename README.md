# PM Project Orchestrator

面向**非技术背景 PM / 业务负责人 / 创始人**的项目总控 Skill。

它的目标不是单纯“帮你写代码”，而是把一个复杂项目从**一句话 idea / 现有产品文档**，一路推进到：

- 产品蓝图
- Web 静态原型页确认
- 架构与模块边界
- 任务总表与进度板
- 分阶段开发
- 用户级测试
- debug 协作
- 完整源码与文档交付

它适合那些：

- 不想被各种底层工程术语淹没
- 但又必须掌握“项目被拆成多少步、做到哪一步、什么时候该介入”
- 希望 AI 在关键技术分歧时，先用**非技术 PM 能读懂的方式**解释差异和建议
- 最终想要的是**可继续迭代的工程**，而不是一次性 demo

## 下载和安装

推荐搭配 [superpower skill](https://github.com/obra/superpowers.git) 使用

```bash
git clone https://github.com/rkbkosp/pm-project-orchestrator.git .agents/skills/pm-project-orchestrator
```

---

## 这是什么，不是什么

### 这是什么

这是一个**单 Agent 项目总控 Skill**。

对外，它只以一个统一助手的身份和你沟通；
对内，它会按阶段模拟：

- 产品分析师
- 交互 / UI 设计师
- 技术方案设计师
- 开发执行者
- 测试助理
- debug 协作助手

### 这不是什么

它不是：

- 只会“从文档直接开写代码”的代理
- 只适合小 demo 的快速原型器
- 让你盲目信任 AI 的黑箱流程

它会把复杂项目拆成你能掌控的流程，并在关键时刻明确告诉你：

- 现在总共有多少步
- 当前做到哪一步
- 这一步产出了什么
- 你现在需不需要介入
- 该怎么测
- 出问题时该怎么协助 AI 修

---

## 适用场景

适合：

- Web 应用
- 移动 App
- Web + 后端
- App + 后端
- 多端工程
- 其它需要完整产品设计、工程落地与迭代文档的软件项目

不建议用于：

- 一次性小 demo
- 几个页面就结束的实验页
- 不关心架构、文档、测试和后续维护的任务
- 只想“尽快有个能跑的东西”，但不需要工程质量的场景

> 这套 Skill 默认面向**复杂项目**。如果只是简单 demo，这套流程通常太重，不划算。

---

## 这个 Skill 会强制执行什么

### 1. 先判断项目类型，再选路径

Skill 不预设项目类型，而是先判断当前项目属于：

- Web
- 移动端
- Web + 后端
- App + 后端
- 多端工程
- 其它软件项目

并向你明确说明：

- 当前判断结果
- 后续采用哪条推进路径
- 为什么这么判断

### 2. 只有一句话 idea 时，必须先进入“会议流程”

如果你只给一句话想法，Skill 不会直接开始写代码。

它会先以**标准会议流程**带你澄清：

- 目标是什么
- 用户是谁
- 关键价值是什么
- MVP 只做什么
- 哪些坚决不做
- 最大风险是什么

只有在产品蓝图成形后，才继续下一阶段。

### 3. 正式编码前，必须先产出 Web 静态原型页

这是强制门禁。

在开始正式编码前，Skill 必须先给你：

- 页面清单
- 页面跳转关系
- 页面结构说明
- **Web 静态原型页**

让你先确认：

- UI 是否正确
- 主流程是否顺畅
- 信息摆放是否合理
- 是否值得进入技术方案与编码阶段

### 4. 必须生成任务总表

Skill 必须始终维护一个你能看懂的“任务总表”。

至少展示：

- 阶段
- 子步骤
- 每步产物
- 当前状态
- 依赖关系
- 是否需要你介入
- 何时可测试

### 5. 测试只在“可运行”时触发

Skill 不会在半成品阶段让你测试。

只有满足以下两个条件，才会正式邀请你测试：

- 一条核心流程或重要功能变更已经完成
- 当前版本**可编译、可运行**

### 6. 关键技术分歧必须解释给你

当不同技术路径会明显影响：

- 开发周期
- 用户体验
- 维护成本
- 扩展性

Skill 必须暂停，并用**表格**向你解释：

- 不同方案分别意味着什么
- 优点
- 风险 / 代价
- 更适合哪种情况
- 推荐方案与理由

### 7. “日报”只在你询问时输出

Skill 可以维护非技术用户阅读版“日报”，但默认不连续轰炸你。

只有你询问时，才整理输出，例如：

- “给我今天的日报”
- “总结一下目前进度”
- “现在做到哪了”

---

## 标准工作流

## 路径 A：只有一句话 idea

1. 项目接收与成熟度判断
2. 会议流程（结构化讨论）
3. 产品蓝图确认
4. Web 静态原型页确认
5. 架构与模块边界设计
6. 任务总表生成
7. 本轮构建范围确认
8. 开发执行与进度透明化
9. 用户级测试
10. debug 协作
11. 交付与迭代建议

## 路径 B：已有产品文档

1. 项目接收与成熟度判断
2. 缺口补齐与蓝图整理
3. Web 静态原型页确认（如果 UI 仍未确认）
4. 架构与模块边界设计
5. 任务总表生成
6. 本轮构建范围确认
7. 开发执行与进度透明化
8. 用户级测试
9. debug 协作
10. 交付与迭代建议

---

## 目录结构

```text
pm-project-orchestrator/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── meeting-flow.md
│   ├── output-templates.md
│   ├── decision-matrix.md
│   └── status-report.md
└── assets/
    ├── codex/
    │   └── AGENTS.example.md
    └── claude/
        └── CLAUDE.example.md
```

---

## 核心产物清单

Skill 在推进过程中，会优先产出下列文档或等价内容：

- `project_intake.md`
- `meeting_notes.md`
- `product_blueprint.md`
- `scope_and_mvp.md`
- `ui_preview.md`
- `screen_specs.md`
- `architecture_overview.md`
- `module_boundary.md`
- `implementation_strategy.md`
- `master_task_board.md`
- `progress_board.md`
- `build_scope_current_round.md`
- `test_intervention_notice.md`
- `uat_scripts.md`
- `acceptance_checklist.md`
- `bug_feedback_template.md`
- `debug_next_actions.md`
- `delivery_summary.md`
- `handoff_notes.md`
- `daily_status_report.md`（仅在用户询问时输出）

---

# 在 ChatGPT Skills 中使用

## 安装方式

1. 准备 `skill.zip`
2. 在 ChatGPT 的 Skills 管理界面上传该压缩包
3. 确认名称显示为 **PM Project Orchestrator**
4. 在项目对话中直接触发

## 推荐触发方式

### 只有一句话 idea 时

```text
我想做一个 [项目一句话描述]。
请用 PM Project Orchestrator 启动会议流程，先帮我把目标、用户、价值、MVP 和风险讲清楚，再继续。
```

### 已有产品文档时

```text
这是我的产品文档/设计文档。
请用 PM Project Orchestrator 先判断项目类型、文档成熟度和应该从哪个阶段开始，然后继续推进。
```

### 要求先出 UI 原型时

```text
在开始写代码之前，请先给我 Web 静态原型页让我确认 UI，再进入正式开发。
```

### 要求持续看见进度时

```text
请始终维护任务总表，按阶段 + 子步骤 + 每步产物展示进度，并告诉我何时该介入测试。
```

---

# 用户该怎么参与

这是给非技术 PM 最重要的一节。

## 你必须介入的时机

### 1. 会议流程阶段
因为需要你确认：

- 目标
- 用户
- 价值
- MVP 范围
- 取舍

### 2. Web 静态原型出来后
因为需要你判断：

- UI 是否正确
- 流程是否顺畅
- 页面是否符合预期

### 3. 技术分歧出现时
因为此时需要你在：

- 速度
- 质量
- 成本
- 可维护性

之间做产品层面的取舍。

### 4. 完成核心流程且当前版本可运行时
因为这时你最适合做用户级测试。

### 5. 你发现 bug 时
你不用分析底层原因，只需要高质量描述现象。

## 你不必介入的时机

- AI 在整理文档结构时
- AI 在做普通实现细节时
- AI 在解决编译问题时
- AI 在修基础测试时
- 还没有形成可运行功能块时

---

# 用户级测试怎么做

当 Skill 说“现在建议你测试”时，它应该同时给你：

- 测试目标
- 前置条件
- 操作步骤
- 预期结果
- 失败后你该反馈什么

典型格式如下：

| 测试编号 | 测试目标 | 前置条件 | 操作步骤 | 预期结果 | 失败后反馈什么 |
|---|---|---|---|---|---|
| UAT-01 | 登录成功 | 已有测试账号 | 打开登录页，输入账号密码，点击登录 | 应进入首页 | 是否报错、报错文字、是否可复现、截图 |

---

# 用户如何协助 debug

你不需要自己分析日志，也不需要判断是谁的问题。

你只要按这个模板反馈给 AI：

## Bug 反馈模板

- 我做了什么：
- 我原本预期：
- 实际发生了什么：
- 是否每次都能复现：
- 有没有看到报错文字：
- 我附上了什么材料：
  - 截图
  - 录屏
  - 控制台输出
  - 其它

你提供的越具体，AI 越容易更快修复。

---

# 常见问题

## Q1. 能不能把 `skill.zip` 直接装进 Codex 或 Claude Code？

不能按 ChatGPT Skills 的方式直接安装。

更实际的方式是：

- ChatGPT：上传 `skill.zip`
- Codex：迁移到 `AGENTS.md`
- Claude Code：迁移到 `CLAUDE.md`

## Q2. 为什么一定要先做 Web 静态原型页？

因为对非技术 PM 来说，最容易失控的不是代码，而是：

- 页面方向不对
- 流程不对
- 信息组织不对

如果这些问题拖到正式编码后才暴露，返工成本会很高。

## Q3. 为什么一定要维护任务总表？

因为你最关心的往往不是“AI 干了多少技术活”，而是：

- 被拆成多少步
- 现在做到哪一步
- 哪一步需要你介入

任务总表正是这件事的统一视图。

## Q4. 我什么时候该问“日报”？

当你想快速了解：

- 今天新增了什么
- 总步骤还有多少
- 当前处于哪个阶段
- 风险是什么
- 下一步是什么

你可以直接说：

```text
给我今天的日报。
```

## Q5. 这个 Skill 会不会太慢？

对简单 demo 来说，会。

但对复杂项目来说，这套流程的价值恰恰在于：

- 先防止方向走偏
- 再防止编码返工
- 再让你在关键节点有控制感

---

# 维护建议

- 当项目类型、团队模式或测试方式变化时，及时更新 `SKILL.md`、`AGENTS.md` 或 `CLAUDE.md`
- 当你发现 AI 在某个环节经常偏航时，把更具体的规则补进项目级说明文件
- 当项目进入新阶段时，把最新蓝图、任务总表、测试文档同步到 `docs/`
- 对长期项目，建议定期整理：
  - `product_blueprint.md`
  - `master_task_board.md`
  - `architecture_overview.md`
  - `uat_scripts.md`
  - `delivery_summary.md`

---

# 快速开始

## 对 ChatGPT

```text
请用 PM Project Orchestrator 帮我推进这个项目。
先判断项目类型和成熟度；如果只是 idea，就先带我开会议把蓝图讲清楚。
```

## 对 Codex

```text
Read AGENTS.md first.
Act as a single project orchestrator for a nontechnical PM.
Start with project-type and maturity assessment.
Do not begin formal coding until a web static prototype is confirmed.
```

## 对 Claude Code

```text
Read CLAUDE.md first.
Act as a single project orchestrator for a nontechnical PM.
Do not begin formal coding until a web static prototype is confirmed.
Only ask me to test when the build is runnable.
```

---

# 官方参考（建议后续自行核对最新版本）

- OpenAI Codex CLI 文档：<https://developers.openai.com/codex/cli>
- OpenAI 关于 Codex / AGENTS.md 的介绍：<https://openai.com/index/introducing-codex/>
- Claude Code Getting Started：<https://code.claude.com/docs/en/getting-started>
- Claude Code Memory / CLAUDE.md：<https://code.claude.com/docs/en/memory>

