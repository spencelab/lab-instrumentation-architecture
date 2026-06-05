# Repository Map

Repository URLs should be added once the architecture repository is created. The names below reflect the current working ecosystem.

## `cambuffer_recorder_ng`

**Role:** High-speed camera acquisition, buffering, and recording.

**Owns:**

- Camera backend interfaces
- XIMEA, FakeCamera, and GenTL-related implementation
- Camera settings and recording-mode behavior
- Raw rolling format and metadata
- Storage-space protection
- Camera-side ROS 2 node lifecycle
- Conversion and inspection utilities directly tied to the recording format

**Does not own:**

- Whole-system orchestration
- Operator GUI workflow
- Triggerbox firmware
- Treadmill control
- Laboratory network configuration

**Likely system dependencies:**

- ROS 2
- Camera SDKs
- OpenCV and media-conversion dependencies
- YAML configuration
- Hardware-trigger input

## `camera_control`

**Role:** Operator GUI and system orchestration.

**Owns:**

- Rig selection
- Launching and stopping system components
- Operator-facing status
- Trigger enable and disable controls
- Treadmill controls presented to the operator
- Coordinated system shutdown
- Future preview and Data Inspector user interfaces

**Does not own:**

- Camera SDK implementation
- Raw recording internals
- Trigger pulse generation
- Treadmill device protocol, unless temporarily colocated during development

## Triggerbox repository

**Exact repository name:** Needs verification.

**Role:** Hardware trigger generation and host communication.

**Expected contents:**

- Microcontroller firmware
- Serial protocol
- Host ROS 2 node
- Enable/disable services
- Trigger timing or counter reporting

## Treadmill-control repository

**Exact repository name:** Needs verification.

**Role:** Treadmill device communication and treadmill-specific control logic.

**Expected contents:**

- Device protocol
- ROS 2 node or API
- Safety limits
- Command and status interfaces
- Launch files

## Data-processing and analysis repositories

Several downstream tools may live separately from acquisition. Add them here as they stabilize.

Possible categories:

- Raw-to-video conversion
- Frame audit and synchronization analysis
- Contact-sheet generation
- Kinematics processing
- Experiment metadata handling
- DeepLabCut workflows

## Repository documentation contract

Each implementation repository should eventually contain:

```text
README.md
AGENTS.md
docs/
  INTERNAL_ARCHITECTURE.md
  CONFIGURATION.md
  TESTING.md
```

The implementation repository explains **how that component works internally**.

This architecture repository explains **how components connect across repository boundaries**.

## Versioning guidance

System-level documents should link to:

- Repository URL
- Default branch
- Released tag, where applicable
- Known compatible versions
- Relevant ROS 2 distribution
- Required hardware or SDK versions

Avoid copying source code into this repository.
