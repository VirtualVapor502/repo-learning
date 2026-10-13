# repo-learning

An agent skill (ZCode / Claude Code / any SKILL.md-compatible coding agent) that turns any code repository into a structured, trackable learning plan.

Paste a repo, answer three quick questions (goal / background / time budget), and get a `LEARNING_PLAN.md` containing:

1. **整体思路 · Overall approach** — how the codebase is organized, what the main end-to-end flow ("spine") is, and which strategy fits: top-down, trace-driven, or bottom-up.
2. **内容拆分 · Breakdown** — 5–12 learning units, each with real file paths, key concepts to look up, a hands-on exercise, dependencies, and honest time estimates. Unit 0 is always "get it running".
3. **番茄打卡 · Punch card** — every unit is pre-split into 25-minute, verb-first 🍅 tasks you tick off one by one; an append-only 打卡记录 table keeps your session streaks.
4. **输出驱动 · Output-driven** — every unit must ship a micro-artifact under `output/` (own-words explainer, annotated diagram, tiny demo) before it counts as done, and the whole plan ends in one capstone 毕业输出 — a blog post, a talk, or a merged PR. Reading without producing doesn't count.
5. **学习计划 · Schedule** — milestones mapped to your weekly budget, self-check questions per unit, and the capstone landing progressively across milestones — all as checkboxes you can tick.

Plans are durable artifacts. Come back in any later session and either **deep-dive** — 「继续 repo-learning 第 3 单元」— or **punch in** — 「打卡 / 今天来两个番茄」— and the skill picks up the next 🍅 task (or walks the unit's code with you), then ticks the box and logs your progress.

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

# Resume in a later session — two modes
继续 repo-learning 第 3 单元        # deep-dive: read this unit's code together
打卡 / 今天来两个番茄               # punch-card: do the next 25-minute 🍅 task
```

The skill triggers on learning intent toward any repo — 学习计划、学习路线、怎么入手这个项目、codebase onboarding、把学习拆成番茄钟, "help me understand this repo" — no slash command needed (but `/repo-learning <repo>` also works where slash invocation is supported).

## What the output looks like

```markdown
## 整体思路
这个仓库是经典的三层结构……主线是 HTTP 请求 → 路由 → 中间件链 → handler → 持久层。
前 1/3 采用自顶向下（先架构后模块），之后切换为追踪式学习（跟着一次真实请求走读代码）。

## 毕业输出
发布一篇《读懂 express》技术博客……完成判定：文章已发布。

## 学习单元
- [ ] **U0 — 跑起来**（预计 1.5h ≈ 3×25min）
- [ ] **U1 — 项目骨架与模块地图**（预计 2h ≈ 4×25min，依赖 U0）
- [ ] **U3 — 请求生命周期：从 router 到 handler**（预计 4h ≈ 8×25min，依赖 U1、U2）
      🍅1 读完 router/index.ts，画出 Layer/Route/Stack 关系图
      🍅2 写一个双中间件 demo，日志验证执行顺序
      输出物：output/u3-request-lifecycle.md — 用自己的话讲清一次请求的完整生命周期
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
