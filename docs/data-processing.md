# Data Processing and Analysis

## Scope

This page describes the boundary between acquisition and downstream processing.

## Acquisition responsibilities

The acquisition system must preserve:

- Raw images
- Reliable metadata
- Camera settings
- Frame timing
- Experiment identifiers
- Software version

## Offline processing responsibilities

Offline tools may perform:

- Raw conversion
- Debayering
- White balance
- Frame auditing
- Cross-camera alignment
- Contact-sheet creation
- Video compression
- DeepLabCut processing
- Kinematic analysis

## Principle

Do not make acquisition depend on expensive analysis.

The recording system should prioritize capturing complete, recoverable data. Processing can be repeated later as methods improve.

## Reproducibility

For important experiments, record:

- Source repository commit
- Conversion-tool commit
- Conversion parameters
- Analysis environment
- Output checksums where practical
