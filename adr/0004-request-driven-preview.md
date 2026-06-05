# ADR 0004: Use request-driven low-rate preview

**Status:** Proposed

## Context

Operators need to inspect camera views for setup, focus, aperture, framing, and gross changes. Real-time video is unnecessary and could burden the network or interfere with recording.

## Decision

Implement preview as controlled frame requests rather than a continuous high-rate ROS image stream.

Support:

- Tiled low-rate overview
- Single-camera inspection
- Current camera settings
- Explicit separation from recording

## Consequences

- Network use remains bounded.
- The GUI controls update rate.
- Preview latency is acceptable.
- Camera-state transitions must be carefully designed.
