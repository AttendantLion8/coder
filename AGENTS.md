# Repository Guidelines

## Project Structure & Module Organization
- `code-rs/` is the primary Rust workspace; make Rust changes here.
- `codex-rs/` mirrors upstream (`openai/codex:main`) and is read-only for this repo.
- `codex-cli/` contains the JS CLI, and `sdk/` hosts the TypeScript SDK.
- `shell-tool-mcp/` contains MCP tooling; `docs/` and `scripts/` hold documentation and automation.
- Tests live under `**/tests/` (e.g., `code-rs/tui/tests`, `sdk/typescript/tests`).

## Build, Test, and Development Commands
- `./build-fast.sh` is the required validation step; it can take 20+ minutes from a cold cache.
- `./pre-release.sh` must be run before pushing to `main`.
- `pnpm run build` / `pnpm run build:dev` / `pnpm run build:quick` build the Rust binaries from `code-rs/`.
- `pnpm run format` checks Prettier formatting for repo-wide JS/MD/YAML.
- Optional Rust sweeps: `cargo nextest run --no-fail-fast` and targeted runs like
  `cargo test -p code-tui --features test-helpers`.

## Coding Style & Naming Conventions
- Rust: fix all warnings (treat them as errors), avoid unused `mut`, and prefer `format!` with inline `{}` variables.
- Do **not** run `rustfmt` (and avoid `pnpm run fix`, which invokes formatting).
- JS/TS: follow Prettier rules from `.prettierrc.toml` and keep formatting consistent with `pnpm run format`.

## Testing Guidelines
- Rust tests live under each crate’s `tests/` directory and are run via `cargo test`.
- TUI snapshots live in `code-rs/tui/tests/snapshots`; update them only when expected.
- VT100 snapshot run: `cargo test -p code-tui --test vt100_chatwidget_snapshot --features test-helpers -- --nocapture`.

## Commit & Pull Request Guidelines
- Use Conventional Commits with an optional scope (e.g., `feat(tui/history): ...`).
- Keep subjects ≤ 72 chars and use imperative tense (`add`, `fix`, `update`).
- Review staged changes before committing (`git --no-pager diff --staged --stat`).
- PRs should include a clear description, linked issues, and screenshots for UI changes.

## Configuration & Safety Notes
- Example configuration lives in `config.toml.example`.
- Keep `codex-rs/` untouched unless explicitly requested; always edit `code-rs/` instead.
