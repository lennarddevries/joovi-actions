# Commitizen Release Action

Automated semantic versioning for Python projects using commitizen.

## Features

- Automated version bumping based on conventional commits
- Updates `pyproject.toml` version field
- CHANGELOG.md generation
- Git tag creation
- Dry-run mode for testing

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `github-token` | GitHub token for pushing changes | Yes | - |
| `python-version` | Python version to use | No | `3.12` |
| `dry-run` | Run in dry-run mode (no actual release) | No | `false` |

## Outputs

| Output | Description |
|--------|-------------|
| `new-release-published` | Whether a new release was published |
| `new-release-version` | Version of the new release |
| `new-release-git-tag` | Git tag of the new release |

## Usage

```yaml
- name: Commitizen Bump
  id: cz
  uses: lennarddevries/joovi-actions/commitizen-release@v3.1.0
  with:
    github-token: ${{ secrets.GH_TOKEN }}

- name: Create GitHub Release
  if: steps.cz.outputs.new-release-published == 'true'
  uses: elgohr/Github-Release-Action@v5
  env:
    GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  with:
    title: ${{ steps.cz.outputs.new-release-git-tag }}
```

## Requirements

The project must have a `pyproject.toml` with commitizen configuration or use the default configuration.

## Conventional Commits

This action requires conventional commits format:
- `feat:` - New features (minor version bump)
- `fix:` - Bug fixes (patch version bump)
- `BREAKING CHANGE:` - Breaking changes (major version bump)
- `chore:`, `docs:`, etc. - No version bump