# Instructions for Coding and Documentation Agents

This repository contains system architecture documentation, not implementation code.

## Before editing

- Read `README.md`, `ARCHITECTURE.md`, and `REPOSITORIES.md`.
- Treat implementation repositories as authoritative for current code behavior.
- Do not invent repository names, node names, service names, device paths, or test results.
- Mark uncertain information as `Needs verification`.
- Preserve the distinction between current behavior and planned behavior.

## Scope

Appropriate changes include:

- Architecture prose
- Repository responsibility maps
- Topology diagrams
- ADRs
- Deployment and testing documentation
- Feature design plans spanning multiple repositories

Do not add copied implementation source trees, Git submodules, generated binaries, datasets, credentials, or hardware SDK files.

## Style

- Write for students and maintainers.
- Prefer explicit ownership and boundaries.
- Use concise diagrams and tables.
- Include reproducible commands where relevant.
- State whether hardware validation occurred.
