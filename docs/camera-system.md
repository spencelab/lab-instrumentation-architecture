# Camera System

## Purpose

The camera system acquires high-rate image streams from multiple cameras and writes recoverable raw recordings with metadata.

## Current design

Each camera computer runs `cambuffer_recorder_ng`, using a backend selected at build or runtime.

Known backends:

- XIMEA xiAPI
- FakeCamera
- GenTL-related support

The recorder applies YAML-defined settings and operates in a named recording mode.

Known modes include:

- Raw 8-bit Bayer GBRG rolling
- Raw 8-bit monochrome rolling
- Hardware-trigger variants

## Data path

```text
Camera sensor
  → camera SDK/backend
  → CBRNG frame handling
  → raw rolling file
  → metadata sidecar
  → offline conversion and audit
```

## Current strengths

- High-rate XIMEA acquisition near 100 Hz
- Flexible fake-camera testing
- Storage-limited continuous recording
- Raw-to-MP4 conversion
- Bayer white-balance support
- Monochrome conversion support
- Graceful converter interruption

## Open architecture work

- Formal lifecycle documentation
- Preview-frame interface
- Unified frame-audit tooling
- Explicit frame identity across computers
- Better experiment-level metadata
- Stable API documentation
