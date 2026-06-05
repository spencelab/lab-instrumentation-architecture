# Design Decisions

This file is a compact index. Detailed decisions live in `adr/`.

| ADR | Decision | Status |
|---|---|---|
| [0001](adr/0001-distributed-repositories.md) | Keep implementation components in separate repositories | Accepted |
| [0002](adr/0002-chrony-for-clock-sync.md) | Use Chrony over the wired network for computer-clock synchronization | Accepted |
| [0003](adr/0003-hardware-trigger-authority.md) | Hardware trigger cadence is authoritative for synchronized acquisition | Accepted |
| [0004](adr/0004-request-driven-preview.md) | Preview should be low-rate and request-driven | Proposed |
| [0005](adr/0005-neutral-architecture-repository.md) | Store system-wide documentation in a neutral architecture repository | Accepted |
| [0006](adr/0006-separate-orchestration-from-device-logic.md) | Keep orchestration separate from device implementation | Accepted |

## Adding a decision

Create a new file:

```text
adr/NNNN-short-title.md
```

Include:

- Status
- Context
- Decision
- Consequences
- Alternatives considered
- Verification or follow-up
