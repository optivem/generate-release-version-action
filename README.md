# Generate Release Version Action

A GitHub Action that converts prerelease versions to release versions by removing prerelease suffixes.

## Description

This action takes a prerelease version (like `v1.0.4-rc`, `v1.0.4-alpha`, `v1.0.4-beta`, or `v1.0.4-preview`) and converts it to a clean release version (like `v1.0.4`) by removing the prerelease suffix.

## Inputs

| Input | Description | Required | Example |
|-------|-------------|----------|---------|
| `prerelease-version` | Prerelease version to convert | Yes | `v1.0.4-rc`, `v1.0.4-alpha`, `v1.0.4-beta` |

## Outputs

| Output | Description | Example |
|--------|-------------|---------|
| `version` | Release version with prerelease suffix removed | `v1.0.4` |

## Usage

```yaml
name: Convert Prerelease to Release
on:
  workflow_dispatch:
    inputs:
      prerelease_version:
        description: 'Prerelease version to convert'
        required: true
        type: string

jobs:
  convert-version:
    runs-on: ubuntu-latest
    steps:
      - name: Generate Release Version
        id: generate-version
        uses: optivem/generate-release-version-action@v1
        with:
          prerelease-version: ${{ inputs.prerelease_version }}
      
      - name: Display Result
        run: |
          echo "Original version: ${{ inputs.prerelease_version }}"
          echo "Release version: ${{ steps.generate-version.outputs.version }}"
```

## Examples

| Input | Output |
|-------|--------|
| `v1.0.4-rc` | `v1.0.4` |
| `v1.0.4-rc2` | `v1.0.4` |
| `v1.0.4-alpha` | `v1.0.4` |
| `v1.0.4-alpha1` | `v1.0.4` |
| `v1.0.4-beta` | `v1.0.4` |
| `v1.0.4-beta3` | `v1.0.4` |
| `v1.0.4-preview` | `v1.0.4` |
| `v1.0.4-preview1` | `v1.0.4` |
| `1.0.4-rc` | `1.0.4` |

## Supported Prerelease Suffixes

- `-rc` (release candidate)
- `-alpha` 
- `-beta`
- `-preview`

All suffixes support optional numeric suffixes (e.g., `-rc1`, `-alpha2`, `-beta3`).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
