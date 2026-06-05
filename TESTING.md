# Testing Strategy

## 1. Testing levels

### Level 1: Static and build checks

Examples:

- Formatting
- Compiler warnings
- Package build
- Interface generation
- Dependency checks

Success at this level does not prove the hardware works.

### Level 2: Software-only tests

Use fake cameras and mocked devices where possible.

Examples:

- FakeCamera resolution and pixel format
- Config parsing
- Recording-file creation
- Converter behavior
- Storage guard logic
- GUI state transitions
- Launch and shutdown logic without hardware

### Level 3: Single-device hardware tests

Examples:

- One XIMEA camera at target settings
- Triggerbox serial connection
- Treadmill command and stop behavior
- Raw file conversion
- Clean device shutdown

### Level 4: Integrated rig tests

Examples:

- Multiple camera computers
- Hardware trigger enabled
- Chrony synchronized
- Central GUI controls all components
- Treadmill integrated
- Coordinated shutdown
- No ghost nodes

### Level 5: Experimental validation

Examples:

- Long-duration run
- Full target frame rate
- Expected storage load
- Cross-camera frame alignment
- Dropped-frame audit
- Recovery from low disk space or device loss
- Verification of final data products

## 2. Minimum change documentation

Every substantive change should record:

- Repository and branch
- Commit
- Machine and OS
- ROS 2 version
- Hardware used
- Commands run
- Build result
- Test result
- Known untested areas

## 3. Camera recording tests

Recommended checks:

- Correct resolution
- Correct pixel format
- Correct frame rate
- Correct trigger mode
- File size growth
- Metadata sidecar creation
- Frame count consistency
- Converter output
- Graceful interruption
- Storage guard behavior

## 4. Synchronization tests

Before a multi-camera run:

- Record `chronyc tracking`.
- Record `chronyc sources -v`.
- Confirm trigger output cadence.
- Confirm each camera receives triggers.
- Compare first valid frame timestamps.
- Compare frame counts.
- Identify missing-frame positions.
- Use trigger counters where available.

## 5. Shutdown tests

A complete shutdown test should verify:

- Recording stops cleanly.
- Trigger output is disabled.
- Camera files finalize.
- Camera nodes terminate.
- Triggerbox host terminates.
- Treadmill stops safely.
- Launch processes terminate.
- `ros2 node list` contains no unexpected nodes.

## 6. Regression tests

Changes to one subsystem should not break:

- FakeCamera build
- Builds without optional SDKs
- Existing YAML profiles
- Raw rolling conversion
- Monochrome recording
- Bayer recording
- Hardware-trigger mode
- System shutdown

## 7. Student testing rule

Students should label results as one of:

- Built only
- Simulated
- Tested with one device
- Tested on full rig
- Used successfully in an experiment

This prevents “works” from becoming an accidental quantum state.
