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

permissions:
  contents: read
  packages: write
  attestations: write
  id-token: write

jobs:
  build:
    uses: nint8835/workflows/.github/workflows/docker-build.yaml@main
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

permissions:
  contents: read
  pull-requests: read
  checks: write

jobs:
  golangci-lint:
    uses: nint8835/workflows/.github/workflows/golangci-lint.yaml@main
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

permissions:
  contents: read
  packages: write

jobs:
  build:
    uses: nint8835/workflows/.github/workflows/earthly-build.yaml@main
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
  pull_request:

permissions:
  contents: read
  security-events: write

jobs:
  lint-actions:
    uses: nint8835/workflows/.github/workflows/lint-actions.yaml@main
```
