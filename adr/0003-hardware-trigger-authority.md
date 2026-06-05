# ADR 0003: Hardware trigger is authoritative for synchronized acquisition

**Status:** Accepted

## Context

System-clock timestamps include transport, buffering, and scheduling delays.

## Decision

Use the hardware trigger cadence, and trigger counters where available, as the authoritative frame-alignment mechanism.

## Consequences

- Cameras can expose on the same physical cadence.
- Host timestamps remain useful for mapping and diagnostics.
- Frame audits should identify missing trigger events rather than relying only on timestamp proximity.
