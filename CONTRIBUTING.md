# Contributing

## Commit & PR conventions

This repo uses [Conventional Commits](https://www.conventionalcommits.org/). Releases are fully
automated by [semantic-release](https://semantic-release.gitbook.io/): the version bump, changelog,
git tag, npm publish, and GitHub release are all derived from commit messages on `main`. There are
no manual version bumps.

### How merging works

PRs are **squash-merged**, and the squash commit message is the **PR title**. That means:

- **Your PR title must be a valid Conventional Commit** — it becomes the single commit on `main`
  that semantic-release reads to decide the next version.
- Individual commits inside the PR are also linted, but on squash they collapse into the PR title.

CI enforces both: a PR cannot be merged if its title (or any commit) is not a valid Conventional
Commit.

### Format

```
type(optional-scope): short summary

optional body (wrap lines at 200 chars)

optional footer (e.g. BREAKING CHANGE: ...)
```

Examples:

- `feat(tools): add knowledge-store import tool`
- `fix: handle empty flow chart on node insert`
- `chore: bump dev dependencies`
- `feat!: drop support for legacy config format`

### Types and their release impact

| Type       | Release | Use for                                 |
| ---------- | ------- | --------------------------------------- |
| `feat`     | minor   | New feature                             |
| `fix`      | patch   | Bug fix                                 |
| `perf`     | patch   | Performance improvement                 |
| `revert`   | patch   | Reverting a previous change             |
| `docs`     | patch   | Documentation changes                   |
| `refactor` | patch   | Code change that neither fixes nor adds |
| `chore`    | none    | Tooling, deps, housekeeping             |
| `test`     | none    | Adding or fixing tests                  |
| `build`    | none    | Build system / packaging changes        |
| `ci`       | none    | CI/CD configuration changes             |
| `style`    | none    | Formatting only (no logic change)       |

**Breaking changes** trigger a **major** release regardless of type: append `!` after the type
(e.g. `feat!:`) or add a `BREAKING CHANGE:` footer.

A PR whose title resolves to a "none" type merges without cutting a release — useful for tooling
and docs-only changes.

## Formatting

All code is formatted with Prettier (project default config). Run `npx prettier --write` on changed
files before pushing; CI checks formatting on every PR.
