# Ensemble Dependency Sync Action

Automatically sync your PHP/Composer dependencies to [Ensemble](https://ensemble.dev) for monitoring updates, security vulnerabilities, and license changes.

## Usage

```yaml
name: Ensemble Dependency Sync

on:
  schedule:
    - cron: '0 9 * * *'  # Daily at 9am UTC
  push:
    paths:
      - 'composer.lock'
  workflow_dispatch:

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: simonhamp/ensemble-action@v1
        with:
          api-key: ${{ secrets.ENSEMBLE_API_KEY }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `api-key` | Your Ensemble API key | Yes | - |
| `ensemble-url` | Your Ensemble instance URL | No | `https://ensemble.dev` |
| `php-version` | PHP version to use | No | `8.2` |
| `working-directory` | Directory containing composer.json | No | `.` |

## Setup

1. Sign up at [Ensemble](https://ensemble.dev) and create an app
2. Copy your API key from the app settings
3. Add `ENSEMBLE_API_KEY` as a secret in your GitHub repository settings
4. Add the workflow file to your repository

## Self-hosted Ensemble

If you're running a self-hosted Ensemble instance, specify your URL:

```yaml
- uses: simonhamp/ensemble-action@v1
  with:
    api-key: ${{ secrets.ENSEMBLE_API_KEY }}
    ensemble-url: 'https://ensemble.yourcompany.com'
```

## Monorepo Support

For monorepos with multiple composer.json files:

```yaml
- uses: simonhamp/ensemble-action@v1
  with:
    api-key: ${{ secrets.ENSEMBLE_API_KEY }}
    working-directory: 'packages/my-app'
```

## License

MIT
