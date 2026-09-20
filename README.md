# @dnd-mapp/config-markdown

[![push main](https://github.com/dnd-mapp/config-markdown/actions/workflows/push-main.yaml/badge.svg?branch=main)](https://github.com/dnd-mapp/config-markdown/actions/workflows/push-main.yaml)
[![npm version](https://img.shields.io/npm/v/@dnd-mapp/config-markdown)](https://www.npmjs.com/package/@dnd-mapp/config-markdown)
[![license](https://img.shields.io/npm/l/@dnd-mapp/config-markdown)](LICENSE)

Shared markdownlint config for all D&D Mapp projects.

## Requirements

- Either `markdownlint-cli2` 0.23 or `markdownlint-cli` 0.49 is a peer dependency and must be installed in your project.
- You only need the CLI you use. Both peer dependencies are optional.

## Installation

Install the config with the CLI of your choice.

```bash
pnpm add -D markdownlint-cli2 @dnd-mapp/config-markdown
```

```bash
pnpm add -D markdownlint-cli @dnd-mapp/config-markdown
```

## Usage

For `markdownlint-cli2`, extend the config from a `.markdownlint-cli2.yaml` file in your project root.

```yaml
config:
    extends: "@dnd-mapp/config-markdown"
```

For `markdownlint-cli`, extend it from a `.markdownlint.yaml` file instead.

```yaml
extends: "@dnd-mapp/config-markdown"
```

Rules that you set next to `extends` override the shared ones.

## Available configs

| Config | Extends path                     | Description                        |
|:-------|:---------------------------------|:-----------------------------------|
| `base` | `@dnd-mapp/config-markdown/base` | The default config for any project |

The package root, `@dnd-mapp/config-markdown`, resolves to `base`.

## What `base` sets

The config enables every default rule of markdownlint and changes the following.

| Rule    | Setting               | Description                                      |
|:--------|:----------------------|:-------------------------------------------------|
| `MD007` | `indent: 4`           | Indents nested list items by 4 spaces            |
| `MD013` | `false`               | Turns off the line length check for wrapped text |
| `MD024` | `siblings_only: true` | Allows repeated headings under different parents |
| `MD060` | `style: aligned`      | Requires table pipes to line up                  |

The config does not set `globs` or `gitignore`. These are options of `markdownlint-cli2`, so set them in your own `.markdownlint-cli2.yaml` file.

## Changelog

Notable changes for consumers of this package are listed in the [changelog](CHANGELOG.md).

## Contributing

Contributions are welcome. See the [contributing guide](CONTRIBUTING.md) for details.

## License

[MIT](LICENSE) © D&D Mapp
