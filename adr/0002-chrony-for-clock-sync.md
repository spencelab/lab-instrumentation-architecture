# ADR 0002: Use Chrony for computer-clock synchronization

**Status:** Accepted

## Context

Multiple camera computers need closely aligned system clocks. Earlier approaches considered PTP and custom ROS time checks.

## Decision

Use Chrony over the wired laboratory network, with one master and camera computers as clients.

## Consequences

- Setup is simpler than a full PTP deployment.
- Approximately 100-microsecond offsets may be achievable in the current environment.
- Clock state must be checked before experiments.
- Hardware trigger remains necessary for deterministic exposure synchronization.
