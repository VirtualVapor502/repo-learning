# Survey cheatsheet

Run from the repo root. Pick by ecosystem — do not run everything mechanically. If a tool is missing, fall back to reading manifests and the tree; never block the survey on a missing tool.

## Repo shape (any language)

```bash
# File count and 2-level dir map
git ls-files | wc -l
git ls-files | awk -F/ '{if (NF>1) print $1"/"$2; else print $1}' | sort | uniq -c | sort -rn | head -30

# Hot files — where the real complexity lives (needs history; use --filter=blob:none clones)
git log --since="1 year ago" --format= --name-only | sort | uniq -c | sort -rn | head -20

# Who maintains what
git shortlog -sn --since="1 year ago" | head -5

# Per-extension LOC (when tokei/cloc unavailable)
git ls-files '*.ts' | xargs wc -l 2>/dev/null | tail -1
```

Docs worth checking before any of the above: `README*`, `CONTRIBUTING*`, `ARCHITECTURE*`, `docs/`, `.github/workflows/*`, `CHANGELOG*`.

## JavaScript / TypeScript

- `package.json`: `scripts` (build/test/dev tell you the workflow), `main`/`bin`/`exports` (entry points), `dependencies` vs `devDependencies`
- Dep tree: `npm ls --depth=0`
- Entry candidates: `src/index.*`, `src/main.*`, `server.*`, `bin/*`
- Circular deps / module graph: `npx madge --circular src`
- Monorepo markers: `workspaces` field, `pnpm-workspace.yaml`, `turbo.json`, `lerna.json`

## Python

- `pyproject.toml` / `setup.cfg` / `setup.py`: `entry_points`/`scripts`, extras
- Deps: `requirements*.txt`, `poetry.lock`, `uv.lock`, or `pip list` in the project env
- Entry candidates: `if __name__ == "__main__"`, console_scripts, `python -m <pkg>`, `src/<pkg>/__main__.py`
- Import graph (if installed): `pydeps <pkg> --show-deps`

## Go

- Packages: `go list ./...`
- Entry candidates: `grep -rl "func main(" --include="*.go" .`
- Dep graph: `go mod graph | head -40`
- Interfaces worth finding: `grep -rn "type .* interface" --include="*.go" | head -20`

## Rust

- Workspace members: read `Cargo.toml` `[workspace] members` or `cargo metadata --no-deps --format-version 1`
- Entry: `src/main.rs` (bin) / `src/lib.rs` (lib), `[[bin]]` targets
- Feature flags shape the architecture — read `[features]`

## Java / Kotlin

- Dep tree: `mvn dependency:tree` or `gradle dependencies`
- Entry: `@SpringBootApplication`, `public static void main`, `application.yml/properties`
- Layout convention: `src/main/java` vs `src/test/java` — module-per-feature or layer-per-folder?

## Tests as documentation

Test names are a cheap behavioral spec — list them instead of reading full files:

```bash
# JS/Vitest/Jest
grep -rEn "^\s*(it|test|describe)\(" src/ tests/ | head -40
# pytest
pytest --collect-only -q | head -40
# go
grep -rn "^func Test" --include="*_test.go" . | head -40
```
