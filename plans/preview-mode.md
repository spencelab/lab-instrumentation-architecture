# Preview Mode Plan

**Status:** Early design

## User need

From the master computer, an operator should be able to inspect current images from all cameras before recording.

## Required modes

### Overview

- Show all cameras in a tiled layout.
- Very low frame rate is acceptable.
- Purpose is to confirm framing and detect obvious changes.

### Single-camera inspection

- Show one selected camera.
- Useful for focus, aperture, exposure, and alignment.
- Higher update rate than overview may be allowed, but real-time video is not required.

## Constraints

- Must not record.
- Must not silently change persistent recording settings.
- Must not saturate the wired network.
- Must not destabilize hardware-triggered acquisition.
- Must report unavailable cameras clearly.

## Proposed architecture

1. GUI requests a preview frame.
2. Camera node applies the current configuration in a preview-safe state.
3. Camera node acquires one frame or a tightly bounded burst.
4. Camera node returns or publishes a compressed or appropriately sized image.
5. GUI displays the result.
6. The system remains ready to exit preview cleanly.

## Open questions

- Service response versus temporary image topic
- Compression format
- Whether preview requires stopping and reconfiguring the camera
- Preview behavior with hardware trigger connected
- Maximum acceptable image size
- Whether all-camera requests run sequentially or in parallel
