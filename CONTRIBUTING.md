# Contributing

Thank you for your interest in contributing to `@dnd-mapp/config-markdown`.

This package is the shared markdownlint config for all D&D Mapp projects. A change here affects every project that extends it, so please keep changes small and deliberate.

## Before you start

Open an [issue](https://github.com/dnd-mapp/config-markdown/issues) to discuss any change beyond a typo fix before you send a pull request. This avoids work on changes that do not fit the goals of the package.

## Development setup

The required tool versions are enforced through `devEngines` and `engineStrict`, so installing with other versions fails.

- Node `24.21.0`
- pnpm `12.4.2`

Install the dependencies with:

```bash
pnpm install
```

Dependency versions live in the `catalog` in `pnpm-workspace.yaml`, which uses `catalogMode: strict`. Add or bump versions there and reference them with `catalog:` in `package.json`.

Newly published releases are held back for three days through `minimumReleaseAge`. You may need to wait before you can bump to a very recent version.

## Changing or adding a config

Configs live in `configs/*.yaml`. The `exports` map in `package.json` exposes each config, and the package root resolves to `base`.

Keep every config limited to markdownlint rules. Do not add options that belong to a single CLI, such as `globs` or `gitignore` from `markdownlint-cli2`, so the config works with both `markdownlint-cli2` and `markdownlint-cli`.

This repository lints itself with the base config. Check and format the repository with these commands.

```bash
pnpm run lint-md
pnpm run format-check
pnpm run format
```

The scripts in `scripts/` are JavaScript files that TypeScript checks with `checkJs`. Run the type check after you change one.

```bash
pnpm run typecheck
```

The `peerDependencies` ranges set the lowest CLI versions that bundle a `markdownlint` release with every rule that the config uses. Raise them when you enable a rule that older versions do not know, because those versions ignore it silently.

When you add or change a rule, update the README in the same pull request.

- Update the "Available configs" table when you add a config.
- Update the "What `base` sets" section when you change the rules of `base`.

## Changelog and versioning

This project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html). Record every notable change for consumers under `[Unreleased]` in `CHANGELOG.md`, using the [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format.

Enabling a stricter rule can make existing consumer projects fail their lint. Treat it as a breaking change and say so in the changelog entry.

## Code style

Follow the rules in `.editorconfig`.

- Use UTF-8 and LF line endings.
- Indent with 4 spaces, or 2 spaces in `package.json` and `pnpm-*.yaml`.
- End every file with a newline and trim trailing whitespace.

Follow these rules for prose, including Markdown files.

- Never hard wrap prose. Write each paragraph or list item on a single line.
- Use US spelling, for example "color" and "behavior".
- Keep every sentence at or under 40 words.
- Pretty print Markdown tables so the columns line up, with alignment markers on every separator line.

## Branches

Create a branch from `main` for each change. Name it `<type>/<short-description>` in lowercase with hyphens between words, for example `feat/add-strict-config` or `fix/table-style`.

Use the same types as for commits.

## Commits

Write commit messages that follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).

```text
<type>(<optional scope>): <description>
```

Use one of these types.

| Type       | Use for                                           |
|:-----------|:--------------------------------------------------|
| `feat`     | A new config or a new rule                        |
| `fix`      | A correction to an existing config or rule        |
| `docs`     | Changes to documentation only                     |
| `refactor` | Changes that do not alter the behavior of configs |
| `build`    | Changes to packaging, dependencies, or tooling    |
| `chore`    | Other maintenance that does not fit above         |

Write the description in the imperative mood, such as "add strict config". Mark a breaking change with `!` after the type or scope, and add a `BREAKING CHANGE:` footer that explains what consumers must do.

## Pull requests

- Keep each pull request to one change.
- Link the issue it addresses.
- Update the changelog and README in the same pull request.
- Use a title that follows the commit convention.

## License

By contributing, you agree that your contributions are licensed under the [MIT license](LICENSE).
