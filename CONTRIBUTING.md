# Contributing to the Architecture Documentation

## Audience

This repository is written for:

- Students joining the instrumentation effort
- Researchers operating the rig
- Developers changing ROS 2 packages
- Maintainers diagnosing system-level failures
- Future lab members trying to understand why the system looks this way

## Documentation rules

1. Prefer tested facts over assumptions.
2. Mark uncertainty explicitly.
3. Do not paste large amounts of source code.
4. Link to the owning repository.
5. Keep system-level and repository-internal details separate.
6. Include commands when they are part of a reproducible workflow.
7. Distinguish present behavior from planned behavior.
8. Update diagrams and prose together.
9. Avoid undocumented machine-specific exceptions.
10. Never record passwords, secrets, private student data, or sensitive experimental data.

## Status labels

Use these labels in prose where helpful:

- **Confirmed**
- **Current design**
- **Planned**
- **Needs verification**
- **Deprecated**

## Pull-request checklist

- Does the change describe the current system?
- Was the affected implementation repository checked?
- Were relevant hardware tests performed?
- Are repository names and links correct?
- Does the change introduce a new cross-repository interface?
- Should an ADR be added?
- Do startup, shutdown, deployment, or testing docs need updates?

## Student workflow

A student making a change should:

1. Read the relevant system page.
2. Read the owning repository's README and internal docs.
3. Identify the boundary of the proposed change.
4. Discuss cross-repository impacts before implementation.
5. Work on a feature branch.
6. Record build and test evidence.
7. Update documentation when behavior changes.

Questions are welcome. Guessing silently is not.
