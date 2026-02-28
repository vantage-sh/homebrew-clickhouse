# Agent Guide: Adding ClickHouse Versions

This repository uses versioned Homebrew formulae in `Formula/` and automated bottle workflows.

## Quick process

1. Pick the target release tag from ClickHouse GitHub releases (for example, `v25.10.6.36-stable`).
2. Get the release SHA from GitHub release assets:
   - `clickhouse-macos-aarch64` (used by current formula pattern)
   - optional: `clickhouse-macos` (x86_64) if formula logic is expanded later.
3. Copy the latest versioned formula file and create `Formula/clickhouse@XX.YY.rb`.
4. Update in the new file:
   - class name (`ClickhouseATXXYY`, e.g. `ClickhouseAT2510`)
   - `url` to the target release asset
   - `sha256` to the matching release digest
   - keep existing install/service/test structure unless there is a release-specific need.
5. Add the new formula name to `audit_exceptions/head_non_default_branch_allowlist.json`.
6. Run local checks and open a PR.

## Commands

List recent releases:

```sh
gh release list -R ClickHouse/ClickHouse --limit 100
```

Inspect one release and copy digest values:

```sh
gh release view v25.10.6.36-stable -R ClickHouse/ClickHouse --json tagName,url,assets
```

## PR expectations in this repo

- Keep the formula-add PR focused (preferably only the new formula file).
- CI (`brew test-bot`) validates formula syntax/build workflow.
- Bottle registration is handled by the `pr-pull` label workflow.

## Follow-up maintenance (separate commit if needed)

- Update aliases in `Aliases/` if changing defaults.
- Update `README.md` version references.
- Mark previous latest formula `keg_only :versioned_formula` when promoting a new latest line.
