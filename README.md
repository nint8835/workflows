# Workflows

Reusable GitHub Actions workflows, to be used by other repos

## `docker-build.yaml`

Handles building and pushing the Docker image for a repo to a container registry (currently just GitHub Container Registry), with good defaults such as caching and artifact attestation.

### Usage

```yaml
name: Build Docker image

on:
  push:
    branches:
      - main

permissions: {}

jobs:
  build:
    uses: nint8835/workflows/.github/workflows/docker-build.yaml@main
    permissions:
      attestations: write # Needed to create attestations
      contents: read # Needed to clone the repository
      id-token: write # Needed to sign attestations
      packages: write # Needed to push to GitHub Container Registry
    with:
      image_name: YOUR_USERNAME/YOUR_REPO
```

## `golangci-lint.yaml`

Handles running of golangci-lint, automatically checking out code and setting up Go.

### Usage

```yaml
name: golangci-lint

on:
  push:
  pull_request:

permissions: {}

jobs:
  golangci-lint:
    uses: nint8835/workflows/.github/workflows/golangci-lint.yaml@main
    permissions:
      checks: write # Needed to post check run results
      contents: read # Needed to clone the repository
      pull-requests: read # Needed to read PR information
```

## `earthly-build.yaml`

Builds and pushes a Docker image via [Earthly](https://earthly.dev/).

### Usage

```yaml
name: Build Docker image

on:
  push:
    branches:
      - main

permissions: {}

jobs:
  build:
    uses: nint8835/workflows/.github/workflows/earthly-build.yaml@main
    permissions:
      contents: read # Needed to clone the repository
      packages: write # Needed to push to GitHub Container Registry
    with:
      target: +my-image
```

## `lint-actions.yaml`

Lints GitHub Actions workflow files using actionlint and zizmor.

### Usage

```yaml
name: Lint Actions

on:
  push:
    branches:
      - main
    paths:
      - .github/workflows/**
  pull_request:
    paths:
      - .github/workflows/**

permissions: {}

jobs:
  lint-actions:
    uses: nint8835/workflows/.github/workflows/lint-actions.yaml@main
    permissions:
      actions: read # Needed to read GitHub Actions information
      contents: read # Needed to clone the repository
      security-events: write # Needed to submit scan results to GitHub
```
