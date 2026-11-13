# dsh-knowledge-graph-releases

Public **release artifacts** for the DSH knowledge graph plugin (`@local/dsh-knowledge-graph`).
The source repository is private; only installers and their manifests are published here.

## What a release contains

| Asset | Purpose |
|---|---|
| `local-dsh-knowledge-graph-<version>.tgz` | The plugin installer (`npm pack`) |
| `release.json` | Machine-readable manifest the plugin reads |
| `SHA256SUMS` | The same digest, for manual `sha256sum -c` |

## How clients use it

The plugin never calls the GitHub API. It reads one static URL:

```
https://github.com/decadez/dsh-knowledge-graph-releases/releases/latest/download/release.json
```

The installer URL is derived from the repository name and the version in that manifest, so a
tampered manifest cannot redirect the download elsewhere. When a newer version exists, the plugin
downloads the installer and compares its SHA256 with the manifest before offering an upgrade.

## Verify an artifact by hand

```bash
curl -fsSLO https://github.com/decadez/dsh-knowledge-graph-releases/releases/latest/download/SHA256SUMS
curl -fsSLO https://github.com/decadez/dsh-knowledge-graph-releases/releases/latest/download/local-dsh-knowledge-graph-<version>.tgz
sha256sum -c SHA256SUMS
```

A digest is not a signature: whoever can publish a release here is the trust boundary.
