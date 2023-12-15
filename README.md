# Imatic Build Action

Builds docker-compose based project images and pushes them to registry.

## Usage in workflow

An example usage of this action in build workflow.

```yaml
name: Build Image

on:
  workflow_call:
  workflow_dispatch:
  push:
    branches: [main]

env:
  REGISTRY: ghcr.io

jobs:
  build_image:
    name: Build Image
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Login to GitHub Container Registry
        uses: docker/login-action@v3
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Build & push
        uses: imatic/imatic-build-action
        with:
          registry: ${{ env.REGISTRY }}
```
