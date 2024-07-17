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
