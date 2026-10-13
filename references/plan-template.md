# LEARNING_PLAN.md template

Copy this structure, replace `{{placeholders}}`, delete sections that don't apply. Write everything in the user's language. Unit count: 5–12. Every unit gets a pomodoro punch-card breakdown (番茄拆解), a hands-on exercise, a self-check question, and a required micro-output (输出物); the whole plan ends in one capstone (毕业输出).

````markdown
# {{Repo name}} 学习计划

> 由 repo-learning 生成于 {{YYYY-MM-DD}}。之后任何会话里说「继续 {{repo}} 第 N 单元」深读，或说「打卡 / 今天来两个番茄」直接做下一个番茄任务。

## 学习目标

{{One paragraph, written as ability not topics: after this plan the user will be able to ___（e.g. 独立实现一个经过 {{spine}} 的完整功能）}}

## 背景

- 语言/框架熟悉度：{{...}}
- 对本仓库已有的了解：{{...}}
- 时间预算：{{e.g. 每天 1h，共 3 周}}

## 整体思路

{{3–6 sentences: 这个仓库是怎么组织的；主线（spine）流程是什么；为什么按这个顺序学（top-down → trace-driven 的切换点在哪里）}}

## 里程碑

| 里程碑 | 覆盖单元 | 目标日期 | 完成标志 |
|---|---|---|---|
| M1 | U0–U2 | {{date}} | {{e.g. 本地能跑通，能画出模块图}} |
| M2 | U3–U6 | {{date}} | {{e.g. 能完整口述一次请求的生命周期}} |
| M3 | U7–U9 | {{date}} | {{e.g. 独立完成练习小功能并通过测试}} |

## 毕业输出

{{The one deliverable that marks the whole plan done, chosen in Phase 0: 发布一篇《读懂 {{repo}}》技术博客 / 一次 20 分钟内部分享 / 一个被合并的 PR / 一份带实测数据的选型结论}}
完成判定：{{objective and checkable, e.g. 文章已发布到 {{platform}}，或 PR 状态为 merged}}
进度锚点：{{e.g. M2 结束时大纲已成稿，M3 开始时初稿完成}}

## 学习单元

### U0 — 跑起来（预计 {{h}}h ≈ {{m}}×25min）
- [ ] 克隆仓库，安装依赖
- [ ] 构建成功
- [ ] 跑通测试套件，记录测试数量：{{n}}
- [ ] 启动服务，用 {{curl / browser}} 触发一个真实请求
- 关键文件：`{{...}}`
- 概念：{{build tool、包管理器的项目特有用法}}
- 番茄拆解：
  - [ ] 🍅1 {{动词开头的任务，一个番茄内可完成，含完成标准}}
  - [ ] 🍅2 {{...}}
- 输出物：`output/u0-{{slug}}.md` — {{e.g. 环境搭建笔记 + 踩过的坑}}
- 自检：{{...}}

### U1 — {{标题}}（预计 {{h}}h ≈ {{m}}×25min，依赖 U0）
- [ ] {{core activity}}
- 关键文件：`{{real paths, ≤10}}`
- 概念：{{要查的术语/模式}}
- 番茄拆解：
  - [ ] 🍅1 {{动词开头，含完成标准，如「读完 X 并画出 Y 图」}}
  - [ ] 🍅2 {{...}}
  - [ ] 🍅{{m}} {{...}}
- 练习：{{动手任务（通常已拆进某个番茄里）}}
- 输出物：`output/u{{n}}-{{slug}}.md` — {{用自己的话解释什么 / 画什么图 / 什么小 demo}}
- 自检：{{学完应该能回答的问题}}

（……依此类推）

## 打卡记录

| 日期 | 单元 | 番茄数 | 输出物 | 备注 / 卡点 |
|---|---|---|---|---|
| | | | | |
````

## Usage notes

- The first unchecked 🍅 inside the active unit is the punch-card resume pointer; the first unchecked *unit* is the plan-level pointer.
- A unit's checkbox may only be ticked after its 输出物 file exists; 打卡记录 (punch log) is append-only — one row per session with the pomodoro count.
- The 毕业输出 is chased progressively: outline by the second milestone, first draft one milestone before the end, finished at the last.
- If the user's budget can't fit all units, cut units from the tail and say so in 整体思路 — don't inflate estimates to fit.
