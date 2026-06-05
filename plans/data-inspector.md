# Data Inspector Plan

**Status:** Concept

## Purpose

Provide experiment-level quality control across cameras and computers.

## Candidate capabilities

- Discover recordings from all participating camera computers
- Read frame metadata without converting full videos
- Identify the first common synchronized frame
- Compare frame counts
- Locate dropped or irregular frames
- Generate contact sheets
- Summarize camera settings
- Record Chrony state
- Produce a machine-readable audit report
- Copy or archive selected summaries centrally

## Architectural principle

Inspection should be offline or low priority. It must not compete with active acquisition.

## Likely components

- Metadata reader library
- Per-recording audit
- Multi-camera alignment tool
- Report generator
- GUI integration
- Archive/export layer

## Open questions

- Authoritative experiment identifier
- Trigger-counter availability
- Central versus distributed file access
- Report format
- Handling partial or interrupted recordings
