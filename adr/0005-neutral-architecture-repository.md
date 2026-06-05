# ADR 0005: Use a neutral system architecture repository

**Status:** Accepted

## Context

System documentation placed in `camera_control` would imply that the GUI repository owns the entire ecosystem.

## Decision

Create a dedicated `lab-instrumentation-architecture` repository containing system-wide documentation only.

## Consequences

- Students have one neutral entry point.
- Cross-repository boundaries are easier to explain.
- Documentation can evolve without changing implementation code.
- Individual repositories still need internal documentation.
