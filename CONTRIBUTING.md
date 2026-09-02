# Contributing

Until Filecoin Pin is imported, this repository is governance-only. Validate a documentation change with:

```sh
git fetch origin main
git diff --check origin/main...HEAD
git diff -- README.md CONTRIBUTING.md SECURITY.md AGENTS.md docs/adr
```

The last command prints this PR's intended changes for scope review. After #4 pins Filecoin Pin, use its recorded Node/pnpm versions and run:

```sh
pnpm install --frozen-lockfile
pnpm test
```

Use a focused branch and PR to `main`. Keep imports, contract changes, and behavior changes separate. Name the first failing behavior test in implementation PRs; include performance evidence only for changed hot paths. Do not merge your own PR without an explicit maintainer exception.

Filecoin Pin is canonical. Add capability through its existing core and CLI seams; adapters depend on those seams and never the reverse. Changes to public compatibility, network defaults, custody, telemetry, releases, or ownership require the authority listed in `AGENTS.md`.
