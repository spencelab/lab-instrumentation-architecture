# Treadmill Integration

## Purpose

The treadmill is part of the experimental apparatus but should remain architecturally separate from camera acquisition.

## Ownership

The treadmill component should own:

- Device communication
- Command validation
- Speed and acceleration limits
- Safe stop behavior
- Status reporting

The control GUI should own:

- Operator controls
- Displayed status
- Inclusion in rig startup and shutdown
- Coordination with experiment workflow

## Launch integration

Planned work includes adding treadmill components to rig launch files.

A rig profile should declare whether treadmill support is:

- Required
- Optional
- Disabled

## Safety requirements

The system should define:

- Maximum allowed command
- What happens on communication loss
- What happens during GUI shutdown
- Emergency-stop procedure
- Whether motion commands latch or expire

These details need verification against the current treadmill implementation.
