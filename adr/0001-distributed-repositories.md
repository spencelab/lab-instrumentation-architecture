# ADR 0001: Keep implementation components in separate repositories

**Status:** Accepted

## Context

The instrumentation ecosystem contains camera acquisition, orchestration, trigger, treadmill, and analysis components with different hardware and release cycles.

## Decision

Keep implementation components in separate Git repositories.

Do not create an umbrella repository containing nested copies or Git submodules merely for documentation.

## Consequences

- Each component can evolve independently.
- Ownership remains clear.
- The ROS 2 workspace can contain multiple sibling repositories.
- System-level documentation must link them coherently.
- Cross-repository changes require explicit coordination.
