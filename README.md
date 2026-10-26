# Proof of Basis for Umbrel

An [Umbrel community app store](https://github.com/getumbrel/umbrel-community-app-store)
with [Proof of Basis](https://github.com/DeGrandis/proof-of-basis): your
bitcoin cost basis and tax records, kept on your node.

## Install

1. On your Umbrel, open the App Store, then **⋯ → Community App Stores**.
2. Paste `https://github.com/DeGrandis/proof-of-basis-umbrel` and add it.
3. Open **Proof of Basis App Store** and install **Proof of Basis**.

It needs an Electrum server on the Umbrel (Electrs or Fulcrum; either
satisfies the `electrs` dependency) and connects to it on its own. If
Ollama is installed, the assistant finds it too. On first open you choose a
password for Proof of Basis itself.

## What's here

```
umbrel-app-store.yml          the store: id "pob", so app ids start with "pob-"
icon.svg                      the app's icon in the store
pob-proof-of-basis/
  umbrel-app.yml              the listing
  docker-compose.yml          the app, pinned to a release image by digest
  data/                       the app's data (one SQLite file), kept by Umbrel
```

The image is `ghcr.io/degrandis/proof-of-basis`, built for amd64 and arm64
from the app's repository. The app reads the node's services from the
environment: `BTCTAX_ELECTRUM_URL` from Umbrel's Electrs/Fulcrum exports,
and `BTCTAX_OLLAMA_URL` from Ollama's, when it's installed.

## Updating to a new release

1. Tag the release in the app's repository (`git tag v0.2.0`); its build
   publishes `ghcr.io/degrandis/proof-of-basis:0.2.0`.
2. Find the multi-arch index digest:
   `docker buildx imagetools inspect ghcr.io/degrandis/proof-of-basis:0.2.0`
3. Update `image:` in `pob-proof-of-basis/docker-compose.yml` and `version:`
   (and `releaseNotes:`) in `umbrel-app.yml`, then push.
