# renovate-config

Shared Renovate configuration for Seamless repositories.

## Usage

To use this configuration in your repository, create a `renovate.json` file with:

```json
{
  "extends": ["github>Seamless-Agency/renovate-config:default"]
}
```

## Configuration

This configuration extends multiple presets from `sanity-io/renovate-config`:

- **base**: Core Renovate settings
- **semantic-commit-type**: Semantic commit message formatting
- **security**: Security update handling
- **strategy**: Dependency update strategies
- **labels**: PR labeling configuration
- **lock-file-maintenance**: Lock file maintenance
- **node-lts**: Node.js LTS version management
- **typescript**: TypeScript-specific settings
- **schedule**: Update scheduling
- **min-age-3days**: Minimum age before updates (3 days)
- **group-recommended**: Grouping recommended updates
- **group-non-major**: Grouping non-major updates
- **workarounds-esm**: ESM compatibility workarounds
- **workarounds-babel-plugin-react-compiler**: React Compiler workarounds
- **dedupe**: Dependency deduplication

The `branding` preset is explicitly ignored.

