# Software and ROS 2 Topology

## 1. Conceptual topology

```text
                         ┌──────────────────────────┐
                         │   Master control PC      │
                         │                          │
                         │  camera_control GUI      │
                         │  launch/orchestration    │
                         │  status and shutdown     │
                         └────────────┬─────────────┘
                                      │ ROS 2 over wired LAN
             ┌────────────────────────┼────────────────────────┐
             │                        │                        │
┌────────────▼────────────┐ ┌────────▼─────────────┐ ┌────────▼─────────────┐
│ Camera PC 1             │ │ Camera PC 2          │ │ Additional PCs       │
│ cambuffer_recorder_ng   │ │ cambuffer_recorder_ng│ │ recorder/control     │
│ camera backend          │ │ camera backend       │ │ nodes as required    │
│ local storage           │ │ local storage        │ │                      │
└────────────┬────────────┘ └────────┬─────────────┘ └──────────────────────┘
             │                        │
             └──────── hardware trigger lines ─────┘
                                      ▲
                                      │
                         ┌────────────┴─────────────┐
                         │ Triggerbox               │
                         │ firmware + host node     │
                         └──────────────────────────┘
```

Treadmill control may run on the master computer or another designated host and is exposed through the same operator GUI.

## 2. Expected node categories

Exact node names should be verified against current source and launch files.

### Control-side

- Camera-control GUI node
- System launcher or process manager
- Triggerbox host node
- Treadmill-control node
- Future preview coordinator
- Future Data Inspector node

### Camera-side

- One camera-recorder node per camera or camera process
- Backend-specific SDK interaction inside the recorder
- Optional lifecycle services
- Recording and status services

## 3. Service and command categories

Current and planned service categories include:

- Launch component
- Stop component
- Configure camera
- Start recording
- Stop recording
- Enable trigger output
- Disable trigger output
- Shutdown node
- Request preview frame
- Query recorder status
- Query disk-space state
- Query frame or timing metadata

The exact service names and message definitions should be documented in each implementation repository.

## 4. Configuration flow

```text
Rig profile
   │
   ├── identifies participating computers
   ├── identifies cameras and device paths
   ├── selects camera YAML files
   ├── enables optional triggerbox support
   ├── enables optional treadmill support
   └── defines launch and shutdown expectations
```

Camera configuration should remain layered:

1. Package or mode defaults
2. Backend defaults
3. Camera-specific YAML
4. Rig-specific selection
5. Explicit command-line override, where supported

The system should print or expose the effective configuration used for a run.

## 5. Startup sequence

The intended sequence is:

1. Verify network and Chrony state.
2. Verify configured device paths.
3. Launch camera nodes.
4. Configure camera nodes.
5. Launch triggerbox host.
6. Launch treadmill control if required.
7. Verify all components report ready.
8. Enable trigger output.
9. Start recording.
10. Monitor storage, node health, and frame timing.

Rig-specific deviations should be documented.

## 6. Shutdown sequence

The intended sequence is:

1. Stop recording cleanly.
2. Disable trigger output.
3. Finalize recording files and metadata.
4. Stop camera nodes.
5. Stop treadmill commands safely.
6. Stop triggerbox host.
7. Stop supporting launch processes.
8. Confirm no ghost ROS 2 nodes remain.

A GUI button labeled “Shutdown system” must perform this sequence or clearly indicate which step failed.

## 7. Failure behavior

The system should prefer explicit degraded states over silent continuation.

Examples:

- Missing camera: mark that camera unavailable and block recording for rigs requiring it.
- Triggerbox unavailable: do not claim synchronized hardware-triggered readiness.
- Low disk space: stop or refuse recording before corrupting the filesystem.
- Node fails to terminate: report the node and process still alive.
- Chrony offset excessive: warn before recording and record the measured state.
- Dropped frames: preserve enough metadata to audit the failure after acquisition.
