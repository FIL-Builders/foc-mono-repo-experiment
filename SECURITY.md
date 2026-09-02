# Security

Do not use a public issue. Target-specific private reporting is not configured here; this blocks security-sensitive release work. Report inherited Filecoin Pin vulnerabilities through [filecoin-project/filecoin-pin private reporting](https://github.com/filecoin-project/filecoin-pin/security/advisories/new) and FOC contract vulnerabilities through the affected FilOzone repository's private reporting. Include impact, affected revision, reproduction, and safe redacted evidence.

Never include private keys, seed phrases, API tokens, payment credentials, signatures, or user file contents. Signer custody remains with the caller. New surfaces must redact those values from logs, errors, telemetry, fixtures, and reports.

Do not treat a successful Calibration, mock, or devnet operation as Mainnet security or release evidence. A security-affecting dependency, custody, network-default, telemetry, or irreversible-action change requires Filecoin Pin maintainer approval and a CLI/MCP maintainer approval before merge.
