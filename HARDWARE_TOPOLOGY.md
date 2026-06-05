# Hardware and Network Topology

## 1. Computers

The system currently uses multiple Linux computers, with camera nodes distributed across them.

Known roles include:

- **Master control computer** — runs the control GUI and coordinates the system
- **Camera computer 1** — runs at least one camera recorder and may also host triggerbox communication
- **Camera computer 2** — runs at least one camera recorder
- **Additional camera or processing computers** — added as the rig expands
- **GPU analysis computers** — used for DeepLabCut and downstream analysis; not necessarily part of acquisition

Hostnames such as `cam1`, `cam2`, or similar should be recorded in rig-specific documentation.

## 2. Cameras

Current confirmed camera work includes XIMEA devices using xiAPI.

Known tested behavior:

- Resolution near 2048 × 700 in a current use case
- Sustained acquisition near 100 Hz
- Raw Bayer 8-bit recording
- Raw monochrome 8-bit recording
- External hardware triggering

Camera-to-computer assignments should be listed in rig profiles rather than hard-coded into system documentation.

## 3. Triggerbox

The triggerbox is a microcontroller-based pulse generator connected by serial to a host computer and by physical trigger lines to cameras.

Key responsibilities:

- Generate stable trigger cadence
- Enable or disable output on command
- Maintain deterministic trigger counting where supported
- Fail safely with output disabled

A known device path has included `/dev/trig2`. Stable udev aliases are preferred over volatile `/dev/ttyUSB*` names.

## 4. Treadmill

The treadmill is controlled by a dedicated software component and presented through the central GUI.

Document per rig:

- Physical connection
- Host computer
- Device path or network address
- Safe speed and acceleration limits
- Emergency-stop behavior
- Shutdown behavior

## 5. Network

The acquisition network uses wired Ethernet for ROS 2 communication and Chrony synchronization.

Design intent:

- Wired network is authoritative for inter-computer synchronization.
- Wi-Fi may remain enabled for Internet access.
- Network interfaces should be configured so route selection does not accidentally move ROS 2 or Chrony traffic to Wi-Fi.
- Firewall and multicast settings must support the selected ROS 2 middleware.

## 6. Time synchronization

One computer acts as the Chrony master for the acquisition network.

Each client should be configured to:

- Prefer or exclusively use the wired master for experiment timing
- Disable conflicting time services
- Report offset and source state
- Step the clock during setup when needed, but remain stable during acquisition

Before recording, capture:

```bash
chronyc tracking
chronyc sources -v
```

Observed offsets near 100 microseconds are encouraging, but every session should be judged from current measurements.

## 7. Storage

High-rate raw recording is storage intensive.

Each recording computer should document:

- Recording filesystem
- Available capacity
- Expected write bandwidth
- Storage guard threshold
- Temporary or rolling-file behavior
- Final archive location
- Data-transfer procedure

Generated movies, frame dumps, and test outputs should live outside tracked source directories or in clearly gitignored paths.

## 8. Power and cabling

Rig documentation should eventually include:

- Camera power
- Trigger cable routing
- USB or PCIe topology
- Treadmill power and emergency stop
- Network switch
- UPS coverage
- Cable labels

This is a current documentation gap.
