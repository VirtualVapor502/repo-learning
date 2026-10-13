# repo-learning

An agent skill (ZCode / Claude Code / any SKILL.md-compatible coding agent) that turns any code repository into a structured, trackable learning plan.

Paste a repo, answer three quick questions (goal / background / time budget), and get a `LEARNING_PLAN.md` containing:

1. **整体思路 · Overall approach** — how the codebase is organized, what the main end-to-end flow ("spine") is, and which strategy fits: top-down, trace-driven, or bottom-up.
2. **内容拆分 · Breakdown** — 5–12 learning units, each with real file paths, key concepts to look up, a hands-on exercise, dependencies, and honest time estimates. Unit 0 is always "get it running".
3. **学习计划 · Schedule** — milestones mapped to your weekly budget, self-check questions per unit, and an append-only progress log — all as checkboxes you can tick.

Plans are durable artifacts. Come back in any later session, say **「继续 repo-learning 第 3 单元」** / *"continue with unit 3"*, and the skill deep-dives that unit with you — reading the code together — then ticks the box and logs your progress.

## Install

Copy this folder into your agent's skills directory:

| Agent | Location |
|---|---|
| ZCode | `~/.agents/skills/repo-learning/` |
| Claude Code | `~/.claude/skills/repo-learning/` |
| Any project (scoped) | `<project>/.agents/skills/repo-learning/` |

No dependencies, no scripts to run — it's a methodology plus templates the agent follows.

## Usage

```
# Chinese
我想深入学习 https://github.com/expressjs/express，目标是能提交 PR，每天能投入 1 小时

# English
Help me learn this codebase — I want to understand the architecture of the repo
in ~/work/my-api. I can spend ~5h/week for a month.

# Resume in a later session
继续 repo-learning 第 3 单元
```

The skill triggers on learning intent toward any repo — 学习计划、学习路线、怎么入手这个项目、codebase onboarding, "help me understand this repo" — no slash command needed (but `/repo-learning <repo>` also works where slash invocation is supported).

## What the output looks like

```markdown
## 整体思路
这个仓库是经典的三层结构……主线是 HTTP 请求 → 路由 → 中间件链 → handler → 持久层。
前 1/3 采用自顶向下（先架构后模块），之后切换为追踪式学习（跟着一次真实请求走读代码）。

## 学习单元
- [ ] **U0 — 跑起来**（预计 2h）
- [ ] **U1 — 项目骨架与模块地图**（预计 3h，依赖 U0）
- [ ] **U2 — 配置与启动流程**（预计 2h，依赖 U0）
- [ ] **U3 — 请求生命周期：从 router 到 handler**（预计 4h，依赖 U1、U2）
      练习：手工跟踪一个 GET /users/:id 请求，在 auth 中间件加日志验证跟踪顺序
...
```

## Files

```
repo-learning/
├── SKILL.md                        # the workflow the agent follows
└── references/
    ├── survey-cheatsheet.md        # per-ecosystem survey commands
    └── plan-template.md            # LEARNING_PLAN.md document template
```

## License

MIT
