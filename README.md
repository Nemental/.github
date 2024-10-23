# .github Repository

This repository contains reusable GitHub Actions workflows to standardize CI/CD processes across projects. These workflows are designed to be flexible and reusable for common tasks like semantic versioning, Docker builds, and more. You can reference them from other repositories to reduce duplication and ensure consistency.

## Available Workflows

### Reusable Workflow for Semantic Release (release.yml)

This workflow automates the semantic versioning and release process for your project using semantic-release. It calculates the next version based on commits and updates the project accordingly.

**Features**
- Automated Version Management: Automatically determines the next version based on commit history (using semantic commit messages).
- Node.js Environment Setup: Configures the environment to run semantic-release.
- GitHub Integration: Pushes new version tags, updates issues, pull requests, and release notes.

| Input | Optional | Default | Description |
| --- | --- | --- | --- |
| node_version | true | 20 | Specifies which Node.js version to use. |

| Output | Description |
| --- | --- |
| version | Specifies which Node.js version to use. |

**Example Usage**
```yaml
jobs:
  semantic:
    uses: nemental/.github/.github/workflows/release.yml@main
    with:
      node_version: 18
```

### Reusable Workflow for Docker Build (build.yml)

This workflow automates the process of building and pushing Docker images to the GitHub Container Registry (GHCR). It simplifies multi-platform Docker builds, tag management, and image publishing.

**Features**
- QEMU Setup: Enables multi-platform support for Docker builds.
- Buildx Setup: Provides advanced Docker build capabilities (cross-platform, caching, etc.).
- Automatic Tagging: Uses the Docker metadata action to generate and manage tags (e.g., latest, version tags).
- GHCR Integration: Pushes Docker images to the GitHub Container Registry.

| Input | Optional | Default | Description |
| --- | --- | --- | --- |
| version | true |  | A tag for the Docker image. |

**Example Usage**
```yaml
jobs:
  docker:
    uses: nemental/.github/.github/workflows/build.yml@main
    with:
      version: "v1.2.3"
```

## Example: Combining Workflows 

The reusable workflows can be combined to automate both version releases and Docker builds in one pipeline. Here’s an example that first runs the semantic-release workflow to determine the version, and then uses that version to build and push a Docker image.
```yaml
name: Release & Build

on:
  workflow_dispatch:

jobs:
  semantic:
    uses: nemental/.github/.github/workflows/release.yml@main

  docker:
    uses: nemental/.github/.github/workflows/build.yml@main
    needs: semantic
    with:
      version: ${{ needs.semantic.outputs.version }}
```

## Reference the Workflow

In your project, reference a workflow by its name and version. You can call the workflow from this repository using the syntax:
```yaml
uses: nemental/.github/.github/workflows/[workflow_name].yml@main
```

## Contribution

If you'd like to contribute additional workflows or improve existing ones, feel free to open a pull request. Contributions are welcome to help expand the variety of reusable workflows in this repository!
