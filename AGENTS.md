# AGENTS.md

Guidelines for agentic coding agents operating in this repository.

## Repository Overview

This is a **GitHub Actions Composite Action** template. The main file is `action.yml`.

## Project Type

- **Language**: YAML (GitHub Actions)
- **Package Manager**: None
- **Testing**: GitHub Actions workflows

## Build / Test Commands

### Running Tests

Tests run via GitHub Actions. The test workflow (`.github/workflows/test.yml`) runs on:

- `push` events
- `pull_request` events

Tests on multiple OSes: `ubuntu-latest`, `macos-latest`, `windows-latest`.

The workflow includes these test scenarios:

1. **Default test**: Run action with default inputs, verify `tq --version` and `tq --help`
2. **TOML parsing**: Create `example.toml` and verify `tq -r -f example.toml 'test.key'` returns correct value
3. **Version input**: Run action with `version: 0.2.1` and `cache: false`, verify exact version
4. **Output formats**: Test JSON and raw output formats

### Running Tests Locally

Use `act` to run the full test workflow. There is no way to run a single test locally.

```bash
act -W .github/workflows/test.yml
act -W .github/workflows/test.yml --platform ubuntu-latest
```

### Linting

The lint workflow (`.github/workflows/lint.yml`) runs on push and pull requests. It uses `yamllint -d relaxed .` to validate all YAML files.

To run locally: `yamllint -d relaxed .`

### Release Process

Automated via `.github/workflows/release-please.yml` - triggered on push to `master` branch, uses "simple" release type.

## Code Style Guidelines

### General Principles

1. **Keep it simple**: Minimal composite action template
2. **YAML format**: 2-space indentation
3. **Descriptive names**: Clear names for inputs, steps, and jobs

### Git Commit Messages

**Required**: Use [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>(<scope>): <description>
```

Types: `fix`, `feat`, `docs`, `chore`, `refactor`, `test`

Examples:
```
feat: add new input parameter
fix: resolve issue with default value
docs: update README
```

### YAML Conventions

- 2-space indentation
- Hyphen `-` for list items
- Quote strings with special characters
- Use anchor aliases (`&anchor`, `*alias`) for reusable fragments

### action.yml Structure

```yaml
name: <action-name>
description: <description>
author: <username>

inputs:
  <input-name>:
    description: <description>
    required: false
    default: <value>

runs:
  using: composite
  steps:
    - name: <step-name>
      uses: <action>
      with:
        <key>: <value>
      shell: bash
      run: |
        <commands>
      env:
        <VAR>: ${{ inputs.<input> }}

branding:
  icon: <icon-name>
  color: <color>
```

### Naming Conventions

- **Action/Input/Job names**: kebab-case
- **Step names**: Title case
- **Environment variables**: SCREAMING_SNAKE_CASE

### GitHub Actions Best Practices

1. Specify `permissions` (principle of least privilege)
2. Pin action versions (e.g., `actions/checkout@v6`)
3. Use `with:` for inputs
4. Use `id:` on steps when referencing outputs

### Error Handling

- Steps fail on errors by default
- Use `if: ${{ always() }}` or `if: ${{ failure() }}` when needed
- Check for required inputs

## File Structure

```
.
├── action.yml
├── .github/workflows/
│   ├── lint.yml
│   ├── test.yml
│   ├── commitlint.yml
│   └── release-please.yml
├── README.md
├── LICENSE
└── version.txt
```

## Common Tasks

### Adding a New Input

1. Add to `inputs:` in `action.yml`
2. Add `with:` in steps using it
3. Update `README.md`

### Adding a Test Case

Add a step in `.github/workflows/test.yml`:

```yaml
- name: Run action with <scenario>
  uses: ./
  with:
    <input>: <value>
```
