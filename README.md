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

This configuration extends multiple presets from [`sanity-io/renovate-config`](https://github.com/sanity-io/renovate-config):

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

## Minimum release age

The inherited `min-age-3days` preset requires ordinary dependency releases to
be at least 72 hours old. Renovate enforces this for `major`, `minor`, and
`patch` updates when the datasource provides a release timestamp.

Renovate does not currently wire release timestamps into `pin` or `pinDigest`
updates. Digest support is datasource-dependent, and lockfile maintenance is
delegated to the package manager. See
[Renovate issue #40288](https://github.com/renovatebot/renovate/issues/40288)
and the
[minimum release age documentation](https://docs.renovatebot.com/key-concepts/minimum-release-age/).

Before merging an affected PR:

1. Compare the proposed version or digest with the base branch. A range-only
   pin may already resolve to the same artifact.
2. For npm packages, verify the version's registry timestamp:

   ```bash
   npm view <package> time --json | jq -r '."<version>"'
   ```

3. For GitHub Action digests, verify the target commit date and signature:

   ```bash
   gh api repos/<owner>/<repository>/commits/<sha> \
     --jq '{committed: .commit.committer.date, verified: .commit.verification.verified}'
   ```

4. Require at least 72 hours for every newly introduced artifact and record the
   evidence in a PR comment. If an artifact is already present on the base
   branch, document that the pin does not introduce new code.

Do not assume that a pending `renovate/stability-days` check for a pin will
resolve automatically while issue #40288 remains open.
