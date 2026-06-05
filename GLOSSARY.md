# Glossary

## Backend

The implementation connecting the recorder to a specific camera API or simulated camera.

## Camera computer

A computer physically connected to and responsible for one or more cameras.

## Chrony

The time-synchronization software used to align computer clocks over the wired network.

## CBRNG

Common shorthand for `cambuffer_recorder_ng`.

## Data Inspector

Planned system for experiment-level frame metadata, synchronization checks, contact sheets, and quality-control summaries.

## FakeCamera

A software camera backend used for development without physical hardware.

## GenTL

A camera transport-layer standard supported or targeted by parts of the acquisition stack.

## Ghost node

A ROS 2 node or associated process that remains alive after the system is expected to have shut down.

## Hardware trigger

An electrical pulse sent to cameras to initiate exposure at a deterministic cadence.

## Master control computer

The operator-facing computer that runs the central GUI and system orchestration.

## Preview mode

A planned low-rate, non-recording mode for viewing current camera images from the central computer.

## Raw rolling format

The high-throughput recording format used by CBRNG, accompanied by metadata.

## Rig profile

A configuration describing which computers, cameras, device paths, and optional components belong to a particular experimental setup.

## Triggerbox

The microcontroller-based hardware and host software responsible for generating and controlling frame-trigger pulses.

## Udev alias

A stable Linux device name such as `/dev/trig2`, used instead of a volatile serial-port name.
