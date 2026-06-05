# Recording and Conversion Pipeline

## Acquisition

Frames are acquired by a camera backend and written in a high-throughput raw rolling format.

## Outputs

A recording should produce:

- Raw frame data
- Metadata sidecar
- Timestamped filenames
- Enough information to determine resolution, pixel format, frame count, and timing

## Conversion

`raw_rolling_to_mp4` converts recordings to viewable video.

Current known behavior includes:

- Bayer decoding
- White-balance gains
- Monochrome support
- Periodic progress output
- Finalization on Ctrl-C where possible

Known white-balance values used in one XIMEA workflow:

- Red: 1.23
- Green: 1.00
- Blue: 1.60

These values are configuration, not universal camera truth.

## Audit

`raw_rolling_info` and related tools should report:

- Frame count
- Dimensions
- Pixel format
- Time range
- Inter-frame intervals
- Missing or irregular frames where detectable

## Data-management principle

Conversion outputs and test frame dumps should not live in tracked source directories.

Use:

- A gitignored local test-output directory
- A dedicated experiment-data path
- Central archive storage
