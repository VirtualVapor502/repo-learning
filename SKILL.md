---
name: repo-learning
description: Turn any code repository into a structured, trackable learning plan — overall approach, module-by-module breakdown, and a scheduled checklist. Use whenever the user wants to learn, study, understand, or deep-dive a codebase/repo/project, or asks for a 学习思路/学习计划/学习路线/怎么入手/读懂这个项目/codebase onboarding, or pastes a repo URL and asks how to approach it, or asks to break their repo learning into 番茄钟/打卡 tasks — even if they never say "learning plan". Also handles return sessions that punch in (打卡) or resume an existing LEARNING_PLAN.md.
---

# Repo Learning Plan

Turn a code repository into a learning plan the user can actually follow and track: an overall approach, a breakdown into units, and a scheduled checklist written to `LEARNING_PLAN.md`. The method is **pomodoro-paced and output-driven**: every unit is pre-split into 25-minute punch-card tasks (番茄拆解), every unit must end in a tangible artifact (输出物), and the whole plan ends in one capstone deliverable (毕业输出) — reading without producing does not count as done. The plan is a durable artifact — later sessions resume from the file, not from memory.

## Workflow

Five phases. Never skip Phase 0. For small repos, compress Phases 1–3 into one pass; for large ones, do them properly.

### Phase 0 — Scope the learning (before reading any code)

Plans fail when they optimize for the wrong goal. Establish four things in one batched round (AskUserQuestion works well, plain questions fine too):

1. **Goal** — contribute features? understand the architecture? take over maintenance? evaluate the tech? master one subsystem?
2. **Background** — familiarity with the language, the domain, and this repo already?
3. **Budget** — hours per week and total horizon ("1h/day for 3 weeks").
4. **Final output (毕业输出)** — what should exist when the plan is done? Suggest one from the goal: contributing → a merged PR; architecture mastery → a published technical blog post or a 20-minute talk; tech evaluation → a short written verdict with measurements. Never leave it undefined — a plan without a final output is just a reading list.

Pomodoro length defaults to 25 minutes; only ask about it if the user volunteers a preference.

If the user already supplied enough of this, state your assumptions in one sentence and move on. Never run a second round of questions unless an answer is impossible to proceed without.

### Phase 1 — Survey the repo

Read enough to see the skeleton, not every file. In order:

1. README, CONTRIBUTING, ARCHITECTURE/docs index, CHANGELOG
2. Project manifest(s): `package.json` / `pyproject.toml` / `go.mod` / `Cargo.toml` / `pom.xml` …
3. Directory tree, 2–3 levels deep
4. Entry points and build/run config (`main`, `cmd/`, `bin/`, Makefile, docker-compose, CI workflows)
5. Tests layout — test names reveal intended behavior better than source comments
6. Git history hot spots — files that change most are where the project's real complexity lives:

```bash
git log --since="1 year ago" --format= --name-only | sort | uniq -c | sort -rn | head -20
```

Per-ecosystem commands (LOC counts, dependency trees, import graphs) are in `references/survey-cheatsheet.md` — consult it when you need a command, don't run everything mechanically. If the repo isn't local yet, clone it first with `git clone --filter=blob:none` (keeps full history for hot-spot analysis without downloading everything). Never block the survey on a missing tool — fall back to reading the manifest and tree.

Keep the findings as a private scratch summary; do not dump raw survey output on the user:
- Tech stack and architecture style (monolith / services / library / plugin; framework; layering)
- Module map: major dirs → responsibility in one phrase each
- The **spine**: the one end-to-end flow that crosses the most of the codebase (e.g. HTTP request → router → middleware → handler → model → persistence → response)

### Phase 2 — Learning approach (整体思路)

Pick one strategy and justify it in one sentence:

| Strategy | When it fits |
|---|---|
| **Top-down** | Large codebase, architecture understanding is the goal: layers first, then modules, then files |
| **Trace-driven** | Contributing / feature work is the goal: follow the spine end-to-end, learn each module as the trace crosses it |
| **Bottom-up** | Small library or algorithm-heavy code: core data structures and utilities first |

For mid-size or larger repos, default to top-down for the first third of the plan, then switch to trace-driven — architecture without tracing stays abstract, tracing without architecture gets lost.

Write a 3–6 sentence narrative: how the repo is organized, what the spine is, why this walking order. This narrative opens the plan.

### Phase 3 — Break into units (内容拆分)

Split the content into 5–12 units. Each unit must be completable in one sitting's worth of pomodoros and must include a hands-on exercise — passive reading does not stick.

**Unit 0 is always "Run it"**: install deps, build, run the test suite, start the thing, trigger one real request. Nothing after this matters if the user cannot execute the code.

For every unit record:
- **Files** — real paths from the actual repo, ≤10 per unit. Never invent a path; if unsure, re-check the tree.
- **Concepts** — terms/patterns to look up ("middleware chain", "WAL", "how this repo does DI")
- **Exercise** — trace one request through the code, draw the module diagram, change something small and predict which test breaks, add a log line at each spine stage, write one test for an uncovered branch
- **Depends on** — prior unit ids
- **Estimate** — honest hours (2–8 typical), calibrated to *this user's* speed, not an expert's
- **番茄拆解** — 3–8 punch-card blocks; one verb-first task per block, sized to a single 25-minute pomodoro, each with a concrete done-criterion ("读完 `router/index.ts` 并画出 Layer/Route 关系图", never "了解 router"). Blocks × 25 min should roughly equal the estimate; a task that can't fit one pomodoro gets split, not squeezed.
- **输出物** — the micro-artifact that proves the unit was learned, written to `output/uN-slug.md` next to `LEARNING_PLAN.md`: an own-words explainer, an annotated diagram, written answers to the unit's 自检 questions ("for me three months from now"), or a tiny demo. A unit's checkbox may only be ticked after its 输出物 exists.

A literal example of one unit entry (see `references/plan-template.md` for the full document template):

```markdown
- [ ] **U3 — 请求生命周期：从 router 到 handler**（预计 4h ≈ 8×25min，依赖 U1、U2）
  - 文件：`src/router/index.ts`、`src/middleware/auth.ts`、`src/routes/user.ts`
  - 概念：middleware 链、路由匹配优先级、错误传播路径
  - 番茄拆解：
    - [ ] 🍅1 读完 `router/index.ts`，画出 Layer/Route/Stack 三者的关系图
    - [ ] 🍅2 写一个双中间件 demo，用日志验证执行顺序
    - [ ] 🍅3 跟踪一次 `GET /users/:id`，把经过的每个函数记进笔记
    - [ ] 🍅4 故意写一个无 handler 的路由，追一次错误冒出的路径
  - 输出物：`output/u3-request-lifecycle.md` — 用自己的话+一张图讲清一次请求的完整生命周期，写给三个月后的自己
  - 自检：一个路由匹配成功但没有 handler 时，错误从哪里冒出来？
```

### Phase 4 — Write the plan

Write `LEARNING_PLAN.md` from `references/plan-template.md`, in the user's language. Location: repo root if writable, otherwise the current working directory; create the sibling `output/` directory to hold the units' 输出物. Then tell the user: where the file is, the milestone dates given their budget, and the two ways to come back — 「继续 express 第 3 单元」(deep-dive) or 「打卡 / 今天来两个番茄」(punch-card).

### Phase 5 — Resume: punch-card or deep-dive

Every later session keys off `LEARNING_PLAN.md`. Two entry modes:

**Punch-card mode (打卡)** — the user says 打卡 / 开始学习 / "今天来两个番茄" / wants short time-boxed work: find the first unchecked 🍅 of the active unit, restate it in one line, then work it together — guide, answer, walk the code — until the block's done-criterion is met. Tick the block, append a row to 打卡记录 (date, unit, pomodoro count, note). If it was the unit's last block, verify the 输出物 file exists before ticking the unit.

**Deep-dive mode** — the user names a unit or asks to understand something: read the key files together, walk the code, answer questions. Do not regenerate the plan. When the unit's exercise and 输出物 are done, tick and log.

In both modes, progress lives in the file, not in anyone's memory.

## Calibration rules

- **Repo > ~100k LOC**: front-load architecture units, keep every file list short, prefer trace-driven exercises that only touch a slice.
- **User is new to the language**: insert a mini-unit before U0 covering only the language features this repo actually uses.
- **Monorepo**: ask which package(s) to learn; plan one package and note the rest as "later".
- **Budget doesn't fit the units**: cut scope (fewer units, spine only) rather than inflating weekly hours.
- **Unit has no natural artifact**: its 输出物 is written answers to the 自检 questions — the floor is written production, never pure reading.
- **毕业输出 lands progressively**: capstone outline exists by the second milestone, first draft one milestone before the end, finished at the last.
- **Write the plan in the user's language** — Chinese request in, Chinese plan out.
