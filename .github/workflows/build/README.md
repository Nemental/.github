# Reusable Workflow for Docker Build

This workflow automates the process of building and pushing Docker images to the GitHub Container Registry (GHCR). It simplifies multi-platform Docker builds, tag management, and image publishing.

**Features**
- QEMU Setup: Enables multi-platform support for Docker builds.
- Buildx Setup: Provides advanced Docker build capabilities (cross-platform, caching, etc.).
- Automatic Tagging: Uses the Docker metadata action to generate and manage tags (e.g., latest, version tags).
- GHCR Integration: Pushes Docker images to the GitHub Container Registry.

**Inputs**
| Input | Optional | Default | Description |
| --- | --- | --- | --- |
| version | true |  | A tag for the Docker image. |

**Example Usage**
```yaml
jobs:
  docker:
    uses: nemental/.github/.github/workflows/build/main.yml@main
    with:
      version: "v1.2.3"
```
