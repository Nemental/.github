# Reusable Workflow for Semantic Release (release.yml)

This workflow automates the semantic versioning and release process for your project using semantic-release. It calculates the next version based on commits and updates the project accordingly.

**Features**
- Automated Version Management: Automatically determines the next version based on commit history (using semantic commit messages).
- Node.js Environment Setup: Configures the environment to run semantic-release.
- GitHub Integration: Pushes new version tags, updates issues, pull requests, and release notes.

**Inputs**
| Input | Optional | Default | Description |
| --- | --- | --- | --- |
| node_version | true | 20 | Specifies which Node.js version to use. |

**Outputs**
| Output | Description |
| --- | --- |
| version | Specifies which Node.js version to use. |

**Example Usage**
```yaml
jobs:
  semantic:
    uses: nemental/.github/.github/workflows/release/main.yml@main
    with:
      node_version: 18
```
