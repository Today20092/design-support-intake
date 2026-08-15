# Capture matrix

Load only the sections matching the project's archetypes. Each signal is a candidate, not a requirement.

## Shared signals

| Signal | Distinguishes | Capture |
|---|---|---|
| App version and build/commit | stale install vs current defect | packaged metadata |
| OS, architecture, runtime | platform or runtime skew | standard runtime APIs |
| Failure stage and bounded error | boundary that failed | cached structured error or stderr tail |
| Configuration state, redacted | configuration vs code defect | allowlisted fields |

## CLI

| Signal | Distinguishes | Capture |
|---|---|---|
| Arguments with sensitive values removed | invocation vs implementation | parsed argument model |
| Exit code and stderr | rejection vs crash | command wrapper |
| Toolchain version | unsupported runtime | version command |

Mechanism: `tool doctor` writing one text or JSON file.

## Desktop application

| Signal | Distinguishes | Capture |
|---|---|---|
| Process/component reachability | UI vs local service failure | cheap health checks and cached state |
| Launch/install mode | source, portable, or packaged defect | application metadata |
| Recent bounded local errors | startup stage or integration failure | in-memory buffer or log tail |
| GPU and driver | rendering vs application logic | OS APIs, only for rendering failures |
| Local crash dump | hard crash site | platform crash facility, only when hard crashes occur |

Mechanism: Help or Settings -> Support report, with preview before copy/save.

## Web service

| Signal | Distinguishes | Capture |
|---|---|---|
| Service and image versions | deployment drift | deployment metadata |
| Component health | failing service boundary | health endpoints |
| Migration/schema version | schema skew | migration store |
| Bounded per-service logs | failure stage | orchestrator logs with redaction |

Mechanism: admin support endpoint or local support command.

## Network or P2P

| Signal | Distinguishes | Capture |
|---|---|---|
| Protocol and peer compatibility | incompatible versions | handshake state |
| Reachability, NAT, relay state | network path vs application logic | built-in probe |
| Firewall or selected port state | blocked vs refused | OS query |
| Connection path with identifiers hashed | peer/path-specific failure | structured connection log |

Mechanism: explicit network diagnostic command or support report.

## Media pipeline

| Signal | Distinguishes | Capture |
|---|---|---|
| Media metadata without file path/name | input edge case vs pipeline | probe output allowlist |
| Codec/encoder version and capabilities | unsupported codec or hardware path | encoder capability query |
| Pipeline stage and stderr tail | exact failing boundary | process wrapper |

Mechanism: offer a report after failure; inspect media only with user consent.

## Library

| Signal | Distinguishes | Capture |
|---|---|---|
| Library and runtime versions | version conflict | manifest and runtime |
| Minimal reproducer | downstream misuse vs defect | issue form link or code block |
| Dependency tree | transitive conflict | package-manager command, only when relevant |

Mechanism: the reproducer is primary; use a generated environment report only when version skew is plausible.

## Privacy review

For every selected field, record:

| Field | Decision served | Source | Classification | Redaction | Available when broken |
|---|---|---|---|---|---|

Treat tokens, credentials, private content, raw identifiers, and full environment dumps as prohibited by default. Prefer allowlists over attempting to scrub arbitrary files.
