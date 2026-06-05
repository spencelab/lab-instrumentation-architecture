# Startup and Shutdown

## Pre-flight checklist

Before launching the software:

- Confirm all required computers are powered and reachable.
- Confirm wired Ethernet links are active.
- Confirm camera, triggerbox, and treadmill cables are connected.
- Confirm stable device aliases exist.
- Confirm sufficient disk space.
- Confirm the correct Git branches or released versions are installed.
- Confirm ROS 2 environment setup is sourced.
- Confirm Chrony is synchronized.

Recommended commands:

```bash
chronyc tracking
chronyc sources -v
df -h
ros2 node list
```

The initial `ros2 node list` should not contain stale recorder, triggerbox, treadmill, or GUI nodes.

## Normal startup

1. Start the central GUI.
2. Select the intended rig profile.
3. Launch the system.
4. Confirm camera nodes are present.
5. Confirm cameras are configured with the intended mode, resolution, exposure, and trigger behavior.
6. Confirm triggerbox host connection.
7. Confirm treadmill connection if used.
8. Confirm storage guard status.
9. Enable trigger output.
10. Begin recording.
11. Verify frame activity and file creation.

## During recording

Monitor:

- Node status
- Disk space
- Trigger state
- Camera errors
- Dropped-frame indicators
- Chrony health if the session is long
- Treadmill status where applicable

Do not restart or reconfigure a camera silently during an active recording.

## Normal shutdown

1. Stop recording.
2. Wait for file finalization.
3. Disable trigger output.
4. Return treadmill to a safe stopped state.
5. Shut down camera nodes.
6. Shut down triggerbox host.
7. Shut down treadmill node.
8. Shut down launch processes.
9. Confirm the GUI reports success.
10. Verify:

```bash
ros2 node list
```

Only intentionally persistent nodes should remain.

## Recovery from ghost nodes

If a node remains after system shutdown:

1. Identify whether the ROS 2 node corresponds to a still-running process.
2. Check the launch-process log.
3. Attempt the component's normal shutdown service.
4. Stop the owning launch process.
5. Use process-level termination only when graceful shutdown fails.
6. Record the failure in an issue with logs.

Avoid launching a second copy on top of the first. Duplicate triggerbox or recorder nodes can produce confusing and unsafe behavior.

## Emergency shutdown

For urgent hardware safety:

1. Disable trigger output.
2. Stop treadmill motion.
3. Stop recording if possible.
4. Remove device power if software control is unresponsive.
5. Preserve logs and partial files for diagnosis.

The emergency procedure should eventually be printed and mounted near the rig.
