---
name: design-support-intake
description: Design privacy-safe support intake for software projects. Use when creating or improving diagnostic reports, support bundles, log collection, crash capture, GitHub issue forms, or maintainer triage flows.
---

# Design support intake

Turn vague bug reports into reproducible, actionable issues. Collect a signal only when it distinguishes plausible causes.

## Workflow

1. **Map failure surfaces.** Read the project overview, manifests, entry points, existing diagnostics, and issue templates. Classify the project using the archetypes in [references/capture-matrix.md](references/capture-matrix.md). List install, startup, configuration, core-operation, integration, and export surfaces that actually exist. Finish when every user-visible failure belongs to a named surface.

2. **Map decisions to signals.** For each surface, list the causes a maintainer must distinguish, then select the smallest signals that separate them. Record `surface -> decision -> signal -> capture source`. Cut signals with no decision. Finish when every signal changes a triage decision and every surface has enough evidence to choose a next step.

3. **Design the support artifact.** Prefer one user-triggered entry point already native to the product: a Help/Settings action, `doctor` command, or admin endpoint. Make it work when dependent components are unavailable. Produce one previewable, copyable or attachable artifact. Finish when a fresh installation and each degraded state can generate the artifact without hidden setup.

4. **Protect the reporter.** Classify every field as public, sensitive, or prohibited. Redact sensitive values before rendering or writing; omit secrets, content, project names, usernames, home paths, tokens, and identifiers unless a demonstrated decision requires a safe transformation. Keep collection local and explicit. Finish when tests prove both required evidence and redaction using realistic sensitive fixtures.

5. **Design issue intake.** Ask first for reproduction steps, expected behavior, and actual behavior. Request the support artifact when available and provide a fallback for startup failures. Make each field serve a triage decision. Preserve blank issues and existing support links unless the project explicitly chooses otherwise. Finish when a reporter can submit a useful issue without a maintainer follow-up for routine environment details.

6. **Verify end to end.** Test the real packaged or deployed entry point where practical, plus degraded states and redaction. Document any environment-only check that automation cannot perform. Finish when the artifact and issue form agree on field names, instructions, privacy, and fallback behavior.

## Constraints

- **Pull over push.** The user initiates collection and reviews what will be shared.
- **Repro outranks logs.** Logs supplement reproduction steps; they do not replace them.
- **Degrade gracefully.** A broken dependency must not prevent diagnostics about that dependency.
- **Evidence before expansion.** Add crash dumps, GPU data, dependency trees, or telemetry only for observed failure surfaces they can distinguish.
- **Repository fit.** Reuse existing commands, UI surfaces, labels, templates, and support channels before adding new ones.
