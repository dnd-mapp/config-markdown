# Contributing to dnd-mapp/config-markdown

This page adds the details of `dnd-mapp/config-markdown` to the [shared contributing guide](https://github.com/dnd-mapp/.github/blob/main/CONTRIBUTING.md). Read that guide first.

This package is the shared markdownlint config for all D&D Mapp projects. A change here affects every project that extends it, so keep changes small and deliberate.

## Checks

This repository lints itself with the base config through the [shared checks](https://github.com/dnd-mapp/.github/blob/main/CONTRIBUTING.md#checks). On top of those, CI runs `typecheck`, which checks the config files of the repository, such as `.prettierrc.ts`, with TypeScript. Run it before you open a pull request:

```bash
pnpm run typecheck
```

## Changing or adding a config

Configs live in `configs/*.yaml`. The `exports` map in `package.json` exposes each config, and the package root resolves to `base`.

Keep every config limited to markdownlint rules. Do not add options that belong to a single CLI, such as `globs` or `gitignore` from `markdownlint-cli2`, so the config works with both `markdownlint-cli2` and `markdownlint-cli`.

The `peerDependencies` ranges set the lowest CLI versions that bundle a `markdownlint` release with every rule that the config uses. Raise them when you enable a rule that older versions do not know, because those versions ignore it silently.

When you add or change a rule, update the README in the same pull request.

- Update the "Available configs" table when you add a config.
- Update the "What `base` sets" section when you change the rules of `base`.

## Changelog and versioning

This project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html). Record every notable change for consumers under `[Unreleased]` in `CHANGELOG.md`, using the [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format.

Enabling a stricter rule can make existing consumer projects fail their lint. Treat it as a breaking change and say so in the changelog entry.

## Releasing

1. Run the [prepare release workflow](../../.github/workflows/prepare-release.yaml) on `main` with the part of the version to bump, for example `gh workflow run prepare-release.yaml -f bump=minor`. It opens the `chore: release X.Y.Z` pull request with auto-merge on.
2. Review and approve the pull request. Once it merges, the `tag` job of the [push workflow](../../.github/workflows/push-main.yaml) creates the annotated tag `vX.Y.Z` on the merge commit.
3. The [release workflow](../../.github/workflows/release.yaml) runs the CI checks, verifies the tag and the changelog, stages the package on npm, and creates the GitHub Release, which opens a discussion in the Announcements category.
4. Find the staged version with `pnpm stage list` and approve it with `pnpm stage approve <id>` and 2FA.

If the staged version is wrong, reject it with `pnpm stage reject <id>`. The same version cannot be staged again until then.
