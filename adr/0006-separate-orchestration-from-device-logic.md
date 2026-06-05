# ADR 0006: Separate orchestration from device logic

**Status:** Accepted

## Context

The central GUI needs to control cameras, triggering, and treadmill behavior.

## Decision

Keep device-specific implementation in the owning repository. Expose stable ROS 2 services, actions, topics, or process interfaces to the orchestration layer.

## Consequences

- Components can be tested independently.
- The GUI remains replaceable.
- Device logic is not duplicated.
- Interface changes must be coordinated and documented.
