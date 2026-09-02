# Agent instructions

## Commands

Before a documentation PR:

```sh
git fetch origin main
git diff --check origin/main...HEAD
git status --short
```

After #4 records the pinned Filecoin Pin baseline, use that baseline's exact runtime, then run:

```sh
pnpm install --frozen-lockfile
pnpm test
```

## Authority

Filecoin Pin is the fixed root/base codebase. Do not import code, create a shared core, add a second canonical CLI, move modules, or replace its migration path without the issue-authorized work and review.

Agents act only under issue or user authorization. Request review only for a mature latest head. Merge only with every policy gate met and explicit merge authorization; no self-merge absent a maintainer exception. Do not transfer repositories or package ownership, enable telemetry, change network defaults, handle signer secrets, or make irreversible/paid actions unless specifically authorized. Keep adapters dependent on Filecoin Pin public/core seams only.

Every PR needs latest-head CI and one maintainer approval. Changes affecting public compatibility, release, custody, telemetry, network defaults, or ownership additionally need one Filecoin Pin maintainer and one CLI/MCP maintainer approval. Until owners are recorded, that gap blocks affected release gates.
