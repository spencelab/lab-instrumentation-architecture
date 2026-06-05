# Spence Lab Instrumentation Architecture

This repository documents the **system-level architecture** of the Spence Lab's experimental instrumentation ecosystem.

It does not contain the source code for the individual instruments or ROS 2 packages. Instead, it explains how the repositories, computers, devices, services, and data products fit together.

The goal is to make the system understandable enough that a new student can answer:

- What are the major components?
- Which repository owns each component?
- What runs on each computer?
- How do cameras, triggering, time synchronization, treadmill control, and data storage interact?
- How should the system be started, tested, and shut down?
- Where should a proposed change be made?
- Which parts of the design are stable, and which are still evolving?

## Start here

1. [ARCHITECTURE.md](ARCHITECTURE.md) — high-level system overview
2. [REPOSITORIES.md](REPOSITORIES.md) — repository responsibilities
3. [SYSTEM_TOPOLOGY.md](SYSTEM_TOPOLOGY.md) — ROS 2 and software relationships
4. [HARDWARE_TOPOLOGY.md](HARDWARE_TOPOLOGY.md) — computers, cameras, trigger hardware, networking, and storage
5. [STARTUP_SHUTDOWN.md](STARTUP_SHUTDOWN.md) — intended operating sequence
6. [TESTING.md](TESTING.md) — verification strategy
7. [CONTRIBUTING.md](CONTRIBUTING.md) — how students and maintainers should update this documentation

## Documentation status

This is an initial architecture baseline assembled from the current development history. Some details are marked:

- **Confirmed** — tested or repeatedly observed
- **Current design** — intended architecture reflected in current work
- **Planned** — agreed direction, not yet fully implemented
- **Needs verification** — plausible but should be checked against live code or hardware

Where this documentation conflicts with current source code, configuration, or measured hardware behavior, the live system wins. Please open an issue or update the relevant page.

## Guiding principle

Each implementation repository should eventually contain its own internal architecture documentation. This repository remains the neutral, system-level map connecting them.
