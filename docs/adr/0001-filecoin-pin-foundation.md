# ADR 0001: Filecoin Pin is the foundation

Status: proposed; requires one Filecoin Pin maintainer and one CLI/MCP maintainer approval.

## Decision

`filecoin-project/filecoin-pin` is the fixed root and base codebase. Its history, `filecoin-pin` package and binary, core/browser/public exports, Action, server, docs, tests, and release semantics remain canonical through the MVP.

The first implementation import pins an audited Filecoin Pin commit. Extend its existing seams before creating a package. The minimum future workspace shape is the Filecoin Pin root plus an optional adapter package; no shared-core registry is introduced.

```mermaid
flowchart LR
  CLI[filecoin-pin CLI] --> Core[Filecoin Pin core]
  MCP[@fil-b/foc-storage-mcp adapter] --> Core
  Compat[foc-cli compatibility entry point] --> CLI
  Migration[Filecoin Pin migration path] --> Core
  Legacy[ipfs2foc] -. reconcile only through .-> Migration
```

Dependency direction is inward: adapters and compatibility entry points may use Filecoin Pin public/core seams; Filecoin Pin never depends on them. `foc-storage-mcp` becomes a thin local adapter. `foc-cli` supplies proven missing UX and may become a post-MVP alias, never a second canonical CLI. Reuse the Filecoin Pin migration path before considering anything from `ipfs2foc`.

## Runtime and compatibility

Use the selected Filecoin Pin baseline's Node and pnpm policy; the current tracker evidence is Node 24+ and pnpm 10.32.1. #3 must refresh and pin those moving inputs before #4. Preserve public contracts by default; incompatible changes need an approved migration and versioning plan. Packages release independently only when their contract and owner are explicit; otherwise `filecoin-pin` remains the release surface.

## Custody, networks, telemetry

No adapter persists, logs, or sends signer material outside the local Filecoin Pin operation path. Signers and secrets remain caller-controlled; redact credentials, tokens, private keys, signatures, and payment credentials from output, errors, telemetry, and issue reports. Default network selection and every irreversible or paid action must be explicit in the invoking surface, show the target network and cost/side effect before execution, and require an affirmative user action. Calibration, mocks, and devnet are not Mainnet evidence.

Telemetry is opt-in where the inherited baseline permits it, carries no file contents or secrets, and must be documented before enabling new collection. Disable telemetry in tests and provide an opt-out in any new surface.

## Governance and consequences

Use focused topic branches and PRs to `main`; separate mechanical imports, contract changes, and behavior changes. Require latest-head CI and one maintainer approval; no self-merge absent an explicit maintainer exception. Hot-path changes require performance evidence. Upstream sync preserves traceability to the pinned Filecoin Pin base.

There is no recorded CODEOWNERS mapping yet. This is an owner gap: no affected package may claim a release gate, and no release/compatibility change may merge, until a Filecoin Pin maintainer and CLI/MCP maintainer are recorded as owners. This ADR itself needs those same two approvals. #1 must be updated if this approved graph changes.

## Non-goals

No code import, generic operation framework, hosted orchestrator, repository transfer, npm ownership transfer, branding transfer, duplicate payment/provider/data-set/upload implementation, or second migration subsystem.
