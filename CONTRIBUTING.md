# Contributing

## Development setup

This repository uses `mise` for local tooling and task orchestration. Assume only `mise` is installed globally.

```bash
mise install
mise run setup
```

`mise run setup` installs project dependencies and writes the git pre-commit hook used by this repository.

## Common tasks

| Goal                                 | Command               |
| ------------------------------------ | --------------------- |
| Format project files                 | `mise run format`     |
| Lint app, Actions, and shell scripts | `mise run lint`       |
| Fix staged files before commit       | `mise run fix:staged` |
| Type-check the site                  | `mise run typecheck`  |
| Build the production bundle          | `mise run build`      |
| Run the full local check suite       | `mise run check`      |
| Generate an SBOM                     | `mise run sbom`       |

> [!NOTE]
> `mise run test` is currently a placeholder task that reports the project has no dedicated test suite yet. Keep running `mise run check` anyway so local validation matches CI.

## Commits

Commits must follow Conventional Commits. Cocogitto enforces this locally and in CI.

Create commits through `mise`:

- `mise exec cocogitto -- cog commit <type> "<message>" [scope]`
- add `-B` for breaking changes
- run `mise run check:commits` to validate commit messages locally

Examples:

- `feat: add new post metadata handling`
- `fix: preserve rss link generation`
- `docs: clarify local preview workflow`

## Pull requests

Before opening a pull request:

- run `mise run check`
- use a Conventional Commit title for the pull request
- update docs when contributor-facing behavior changes
- keep changes focused and small when possible

## Releases

Releases are managed through `mise`, Cocogitto, and GoReleaser.

- `mise run release:version` creates the next version and tag
- `mise run release:check` validates release configuration
- `mise run release:verify` runs the release pipeline locally in verification mode
- push the resulting commit and `v*` tag to trigger the release workflow
