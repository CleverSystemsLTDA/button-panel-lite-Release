# Button Panel Lite — Release Feed

This repo is the **public update feed** for the Button Panel Lite auto-updater. It intentionally
holds **no source code**: every release here is a build artifact, published automatically by CI
from the private source repo.

- **Source:** `CleverSystemsLTDA/button-panel-lite` (private)
- **Published by:** `.github/workflows/deploy-prod.yml` in that repo, on every `alpha-*`,
  `beta-*` and `v*` tag push, authenticated with the `RELEASES_GH_TOKEN` secret.
- **Consumed by:** the launcher on every panel, which reads it anonymously. No token ever ships
  to a customer.

## Layout

- **Releases:** one per tag, holding `button-panel-lite-x64.zip` and `button-panel-lite-x86.zip`.
- **`channels/<channel>.json`:** one manifest per channel (`stable`, `beta`, `alpha`). It names
  the version that channel should run, plus each zip's URL, size and SHA-256.

Clients poll
`https://raw.githubusercontent.com/CleverSystemsLTDA/button-panel-lite-Release/main/channels/<channel>.json`.

## Channels

| Tag | Version | Channel |
|---|---|---|
| `v1.4.0` | `1.4.0` | stable |
| `beta-1.4.0b2` | `1.4.0b2` | beta |
| `alpha-1.4.0a1` | `1.4.0a1` | alpha |

A release updates its own channel's manifest. It also updates every less stable channel that is
on an older version, so beta and alpha panels never get stuck behind stable.

**Don't edit the manifests by hand.** CI owns them. The design is in
`docs/AUTO_UPDATE_DESIGN.md` in the source repo.
