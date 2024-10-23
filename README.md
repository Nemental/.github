# .github Repository

This repository contains reusable GitHub Actions workflows to standardize CI/CD processes across projects. These workflows are designed to be flexible and reusable for common tasks like semantic versioning, Docker builds, and more. You can reference them from other repositories to reduce duplication and ensure consistency.

## Available Workflows

- [Automated release and changelog with semantic-release](/.github/workflows/release/README.md)
- [Docker build and push](/.github/workflows/build/README.md)

## Example: Combining Workflows "Release" and "Build"

The reusable workflows can be combined to automate both version releases and Docker builds in one pipeline. Here’s an example that first runs the semantic-release workflow to determine the version, and then uses that version to build and push a Docker image.
```yaml
name: Release & Build

on:
  workflow_dispatch:

jobs:
  semantic:
    uses: nemental/.github/.github/workflows/release/main.yml@main

  docker:
    uses: nemental/.github/.github/workflows/build/main.yml@main
    needs: semantic
    with:
      version: ${{ needs.semantic.outputs.version }}
```

## Reference the Workflow

In your project, reference a workflow by its name and version. You can call the workflow from this repository using the syntax:
```yaml
uses: nemental/.github/.github/workflows/[workflow_name]/main.yml@main
```

## Contribution

If you'd like to contribute additional workflows or improve existing ones, feel free to open a pull request. Contributions are welcome to help expand the variety of reusable workflows in this repository!
