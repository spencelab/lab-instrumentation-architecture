# System Architecture

## 1. Purpose

The instrumentation ecosystem supports high-speed, synchronized behavioral recording and related experimental control. Its current center of gravity is a multi-computer ROS 2 camera-recording system, with additional trigger, treadmill, time-synchronization, control-GUI, conversion, and analysis components.

The architecture is intentionally distributed:

- Camera acquisition happens close to each camera.
- Recording nodes own camera-specific acquisition and storage behavior.
- A central control layer coordinates launch, configuration, recording, and shutdown.
- Hardware triggering provides deterministic frame timing.
- Chrony provides computer-clock synchronization across the wired network.
- Recorded raw data is converted and audited after acquisition.

## 2. Major subsystems

### 2.1 Camera acquisition and recording

The `cambuffer_recorder_ng` repository contains the primary ROS 2 camera-recording package.

Current responsibilities include:

- Camera backend abstraction
- XIMEA camera support through xiAPI
- Fake camera support for development and testing
- GenTL support or preparation for GenTL-compatible devices
- YAML-driven camera configuration
- High-rate raw rolling recording
- Storage-space guarding
- Camera-specific lifecycle and shutdown behavior
- Conversion utilities for recorded raw data

Current known recording modes include raw 8-bit Bayer and monochrome rolling modes.

### 2.2 System control and orchestration

The `camera_control` repository contains the operator-facing control GUI and increasingly acts as the orchestration layer for the broader system.

Current or emerging responsibilities include:

- Selecting a rig profile
- Starting and stopping camera nodes
- Starting and stopping supporting nodes
- Coordinating trigger output
- Displaying process or node status
- Integrating treadmill controls
- Performing system-level shutdown
- Eventually supporting preview and inspection workflows

This repository should orchestrate other components without absorbing their internal implementation.

### 2.3 Trigger generation and host control

A triggerbox subsystem provides hardware frame triggers, currently at approximately 100 Hz, with a possible future target of 250 Hz.

The trigger architecture includes:

- Microcontroller firmware generating deterministic hardware pulses
- A host-side ROS 2 node communicating with the triggerbox over serial
- Services or commands to enable and disable trigger output
- Planned or partial support for exposing trigger counters or timing information

Hardware trigger timing is the primary synchronization mechanism for image exposure. Computer timestamps are used for mapping, auditing, and cross-system coordination.

### 2.4 Time synchronization

Chrony synchronizes participating computers over the wired laboratory network.

Current design goals:

- One master computer provides time to camera computers.
- Camera computers use the wired master as their primary time source.
- Wi-Fi remains available for Internet access but should not be the synchronization path.
- Typical observed synchronization has approached approximately 100 microseconds under favorable conditions.
- ROS 2 timestamps remain computer-clock timestamps and are not a replacement for hardware trigger identity.

### 2.5 Treadmill control

Treadmill functionality is being integrated into the same operator GUI used for camera-system control.

The treadmill subsystem should remain separable from camera acquisition while exposing a controlled system-level interface.

Expected boundaries:

- Treadmill-specific protocol and safety logic belong in the treadmill repository or package.
- `camera_control` owns operator interaction and orchestration.
- Launch integration should make treadmill support optional by rig.

### 2.6 Data conversion and audit

Recorded raw rolling files are accompanied by metadata sidecars and can be converted to MP4.

Known utilities include:

- `raw_rolling_to_mp4`
- `raw_rolling_info`
- Frame-audit or cross-camera comparison tools, some of which may still be evolving

The conversion path supports:

- Bayer decoding and white balance
- Monochrome output
- Progress reporting
- Graceful finalization on interruption
- Inspection of frame count and timing metadata

### 2.7 Future preview and data-inspection layer

A future preview mode is intended to provide very low-rate live images at the master computer without competing with recording.

Current design direction:

- Preview is not a continuous high-rate image stream.
- The GUI requests frames at a controlled, low rate.
- Preview should apply the current camera settings.
- Operators should be able to view all cameras as a tiled overview and inspect one camera at higher usefulness for focus and aperture adjustment.
- Recording and preview modes must remain clearly separated.

A broader Data Inspector is also planned for multi-camera frame metadata, synchronization checks, contact sheets, and experiment-level quality control.

## 3. Architectural boundaries

### Recording nodes own

- Camera SDK interaction
- Frame acquisition
- Camera settings application
- Camera-local buffering
- Recording formats
- Camera-local failure reporting

### Control GUI owns

- Operator workflow
- Rig selection
- Process or node orchestration
- System start and shutdown sequence
- Display of status and errors
- Coordination across repositories

### Triggerbox owns

- Pulse generation
- Hardware-level trigger cadence
- Trigger counter generation, where supported
- Safe enable and disable behavior

### Time synchronization owns

- Alignment of computer clocks
- Monitoring of clock offset and source health

### Offline tools own

- Conversion
- Frame audits
- Cross-camera comparisons
- Contact sheets
- Data-integrity summaries

## 4. Core invariants

1. Recording behavior must not silently change when adding GUI or preview features.
2. Hardware-triggered acquisition remains the authoritative frame cadence for synchronized recording.
3. Clock synchronization supports timestamp comparison but does not replace trigger-based alignment.
4. A node that reports successful shutdown must actually terminate or clearly report why it remains alive.
5. Configuration must remain explicit and version-controlled.
6. Optional hardware should not prevent unrelated packages from building when its SDK is absent.
7. Raw data and metadata must remain recoverable even when conversion is interrupted.
8. System-level orchestration must not create duplicate or ghost nodes.
9. Hardware validation must be distinguished from compilation or simulation success.

## 5. Current maturity

| Area | Status |
|---|---|
| XIMEA high-rate acquisition | Confirmed working |
| Fake camera backend | Confirmed working |
| Raw rolling recording | Confirmed working |
| Storage guard | Implemented and tested |
| Monochrome conversion | Implemented and tested |
| Multi-PC hardware-triggered recording | Confirmed working |
| Chrony synchronization | Confirmed working |
| Unified control GUI | Working and actively evolving |
| Triggerbox shutdown integration | Improved; verify current branch behavior |
| Treadmill GUI integration | Working in current development |
| Launch-level treadmill integration | Planned |
| Preview mode | Planned |
| Data Inspector | Planned |
| Complete cross-repository documentation | This repository begins that work |
