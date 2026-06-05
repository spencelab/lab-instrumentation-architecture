# Triggering and Synchronization

## Two different synchronization problems

The system separates:

1. **Exposure synchronization** — controlled by hardware trigger pulses
2. **Computer-clock synchronization** — controlled by Chrony

These mechanisms support each other but are not interchangeable.

## Hardware trigger

The triggerbox distributes pulses to cameras. At 100 Hz, the nominal interval is 10 ms. A possible 250 Hz future mode would use a 4 ms interval.

A trigger counter, when available, is the cleanest frame identity because it can reveal exactly where a camera missed a pulse.

## Computer timestamps

Each camera computer timestamps acquired frames using its synchronized system clock.

These timestamps help:

- Compare systems
- Map acquisition to other events
- Audit first-frame alignment
- Diagnose transport or buffering delay

They may include camera, transport, buffering, and scheduling latency.

## Chrony

The wired master clock should be the primary source during acquisition.

Before experiments:

```bash
chronyc tracking
chronyc sources -v
```

Store the output with experiment metadata where practical.

## Future improvement

Record, per frame where feasible:

- Trigger counter
- Camera timestamp
- Host receive timestamp
- Host write timestamp
- Dropped-frame indicators

This would turn timing archaeology into timing science.
