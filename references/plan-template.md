# LEARNING_PLAN.md template

Copy this structure, replace `{{placeholders}}`, delete sections that don't apply. Write everything in the user's language. Unit count: 5–12. Every unit gets a hands-on exercise and a self-check question.

````markdown
# {{Repo name}} 学习计划

> 由 repo-learning 生成于 {{YYYY-MM-DD}}。之后任何会话里说「继续 {{repo}} 第 N 单元」即可续学。

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

## 学习单元

### U0 — 跑起来（预计 {{h}}h）
- [ ] 克隆仓库，安装依赖
- [ ] 构建成功
- [ ] 跑通测试套件，记录测试数量：{{n}}
- [ ] 启动服务，用 {{curl / browser}} 触发一个真实请求
- 关键文件：`{{...}}`
- 概念：{{build tool、包管理器的项目特有用法}}
- 自检：{{...}}

### U1 — {{标题}}（预计 {{h}}h，依赖 U0）
- [ ] {{core activity}}
- 关键文件：`{{real paths, ≤10}}`
- 概念：{{要查的术语/模式}}
- 练习：{{动手任务}}
- 自检：{{学完应该能回答的问题}}

（……依此类推）

## 进度日志

| 日期 | 单元 | 实际用时 | 备注 / 卡点 |
|---|---|---|---|
| | | | |
````

## Usage notes

- Checkboxes are the resume pointer: the first unchecked unit is where the next session starts.
- The 进度日志 (progress log) is append-only; add a row when a unit's exercise is done, then tick its checkbox.
- If the user's budget can't fit all units, cut units from the tail and say so in 整体思路 — don't inflate estimates to fit.
