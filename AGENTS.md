# AGENTS.md

## What this is

`domain-supervisor` is a tiny npm library (v0.3.1) that runs a function inside a Node `domain` and restarts it on uncaught exceptions. Dormant since 2014-12-17.

## Stack

- JavaScript (ES5, CommonJS). No runtime dependencies, no dev dependencies.
- Uses Node's built-in `domain` module, which Node documents as deprecated. It still ran on Node 22 when checked on 2026-11-20.

## Layout

- `index.js`: exports `Supervisor` and `Process`.
- `src/supervisor.js`, `src/process.js`: the library.
- `test/index.js`, `test/process1.js`: a manual test script.
- `docs/STATUS.md`: current state.

## Commands

- Install: nothing to install (`npm install` is a no-op).
- Test: `npm test` (runs `node test/`). It is designed to end by crashing on purpose after four errors, so a stack trace and non-zero exit are expected. There is no assertion library and no pass or fail summary.
- Run: no app; it is a library.

## Rules

- Add or update tests with every change. If a change cannot be tested, say why in the pull request.
- Never commit secrets: keys, tokens, passwords, `.env` files. Use placeholders such as `sXXXXXXXX`.
- Use Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`).
- Keep `docs/STATUS.md` current when behaviour or tooling changes.

## What agents may and may not do

- May: fix bugs, improve docs, add tests, open pull requests against `master`.
- May not, without Steven: archive or delete the repo, publish to npm or any registry, rewrite git history, change the license, or merge their own pull requests.
