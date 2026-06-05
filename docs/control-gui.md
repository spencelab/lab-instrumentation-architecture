# Control GUI and Orchestration

## Purpose

The control GUI provides a single operator-facing surface for launching, monitoring, controlling, and shutting down the rig.

## Current capabilities

- Camera-system launch controls
- Rig-profile selection
- Trigger output controls
- Treadmill controls
- System shutdown workflow
- Log output

## Architectural role

The GUI should coordinate components without embedding their internal device logic.

It may:

- Start a camera node
- Request a recording state
- Display a camera error
- Stop a triggerbox host
- Request treadmill motion through a defined interface

It should not:

- Implement xiAPI frame acquisition
- Generate trigger pulses
- Reimplement treadmill communication
- Parse raw recording files during normal operation

## Current risks

- Ghost processes after shutdown
- Duplicate node launches
- Tight coupling to repository-specific launch details
- UI state diverging from actual node state
- Rig configuration becoming scattered

## Design direction

Use rig profiles as the central declaration of what belongs to a system.

The GUI should report:

- Requested state
- Actual observed state
- Last command result
- Failure reason
- Whether hardware validation has occurred
