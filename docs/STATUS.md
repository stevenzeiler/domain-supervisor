# Status

Last checked: 2026-11-20 (github-audit pass 02).

## What works

- Ran `node test/` on Node 22.23.5: the process was restarted after errors and then crashed on purpose, matching the test's design.
- Zero dependencies, so nothing to rot.

## What's broken or unknown

- The Node `domain` module is deprecated upstream; behaviour in future Node releases is not guaranteed.
- `npm test` has no assertions, so it cannot report a regression automatically.
- `package.json` has an empty `author`.
- Not confirmed whether v0.3.1 is on the npm registry (not checked).

## What's next

- Steven's call: leave as a dormant reference, or archive.
- If kept alive: turn `test/` into real assertions and add CI.

## Not yet from the standard

- CONTRIBUTING.md
- SECURITY.md
- `.editorconfig`
- `.github/` issue and pull request templates
- Dependabot config
- `ci.yml` with a gitleaks secret scan
- Rename the default branch from `master` to `main`
- CloudEvents catalog (only if the repo ever emits events)
- Product ONE-PAGER

LICENSE was added in this pass because `package.json` already declared ISC.
