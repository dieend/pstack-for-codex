# Release evaluation evidence

This directory is the release ledger for `pstack-for-codex` version `0.5.0`, derived from upstream pstack `0.15.29` at `d1453c11d1dde9714d4c313c97d3a68432265c7f`. The immutable upstream file inventory is [`../upstream.lock.json`](../upstream.lock.json); [`cases/coverage.yaml`](cases/coverage.yaml) maps all 56 upstream skills and all 23 upstream playbooks, while [`cases/representative.yaml`](cases/representative.yaml) covers direct, indirect, incomplete-input, negative-trigger, unsupported-capability, setup, hook, and connector boundaries.

## Recorded environment

| Evidence | Verdict |
|---|---|
| Codex | `codex-cli 0.144.1` observed during the 2026-10-21 clean installation and teardown test. |
| Runtimes | Node.js `26.12.0` and Bun `1.3.8`, selected for the test process only. The machine default was not changed. |
| Models | No model inventory was exposed by the exercised plugin CLI. Actual model names and effort pairs are therefore **unverified/inherited**, not claimed. Setup tests cover supplied observable-model fixtures and unsupported pairs. |
| Permissions | Offline verification used the host's observable local process permissions. No live connector permission or model-generated write was exercised. Installed smoke uses only a temporary `CODEX_HOME` and temporary marketplace. |
| Offline tests | `npm run verify:offline` checks the baseline, static plugin, lifecycle, tooling, Benny fake adapters, and documentation without installing into a Codex profile. `npm run verify` remains an alias for this offline-only target. |
| Installed behavior | The temporary profile test adds a local marketplace, installs and validates the package, runs setup and hook checks, then removes the installation. It does not claim prompt-time discovery or model dispatch. |
| Benny canaries | `not-run`: both automation descriptors remain `PAUSED`. Read-only, test-channel triage, repro-only, bounded-fix, concurrent-race, and ambiguous-write canaries require operator-owned real adapters before activation. |

## Release disposition

All 57 registered skills are explicit-only. All 56 upstream skills and 23 playbooks have offline-contract coverage and applicable authority, capability, and negative-trigger boundaries. These checks do not prove model behavior. Connector- and trust-dependent live activation is deferred, with the automation tasks paused. Polling latency, hook trust, connector availability, model diversity, and Bun availability remain declared limitations.

Run `npm test` (or `npm run verify:release`) for the mandatory release gate. It runs offline verification followed by the installed-profile smoke and fails closed when the `codex` prerequisite is unavailable. A release is blocked by any failed test, missing coverage row, stale compatibility report, residual temporary profile/cache, unpaused Benny descriptor, or an unverified live-activation claim.
