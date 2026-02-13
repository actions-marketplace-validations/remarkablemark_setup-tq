# setup-tq

[![GitHub Release](https://img.shields.io/github/v/release/remarkablemark/setup-tq)](https://github.com/remarkablemark/setup-tq/releases)
[![test](https://github.com/remarkablemark/setup-tq/actions/workflows/test.yml/badge.svg)](https://github.com/remarkablemark/setup-tq/actions/workflows/test.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

⚙️ Set up GitHub Actions with [tq](https://github.com/cryptaliagy/tomlq) (tomlq).

## Quick Start

```yaml
on: push
jobs:
  setup-tq:
    runs-on: ubuntu-latest
    steps:
      - name: Setup tq
        uses: remarkablemark/setup-tq@v1

      - name: Show project version
        run: tq -f pyproject.toml 'project.version'
```

## Usage

**Basic:**

```yaml
- uses: remarkablemark/setup-tq@v1
```

See [action.yml](action.yml)

## Inputs

### `version`

**Optional**: The tq binary [version](https://github.com/cryptaliagy/tomlq/releases). Defaults to [`0.2.2`](https://github.com/cryptaliagy/tomlq/releases/tag/0.2.2):

```yaml
- uses: remarkablemark/setup-tq@v1
  with:
    version: 0.2.2
```

### `cache`

**Optional**: Whether to cache the tq binary. Defaults to `true`:

```yaml
- uses: remarkablemark/setup-tq@v1
  with:
    cache: false
```

## License

[MIT](LICENSE)
