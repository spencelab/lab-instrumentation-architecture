# Deployment and Environment

## 1. Operating systems

Current development spans Ubuntu 22.04 and Ubuntu 24.04 systems, with some historical Ubuntu 18.04 analysis machines.

The acquisition stack should explicitly document:

- Supported Ubuntu version
- Supported ROS 2 distribution
- Compiler version
- Camera SDK version
- Required kernel or USB settings
- Middleware configuration

## 2. ROS 2 workspace layout

Typical layout:

```text
~/ros2_ws/
├── src/
│   ├── cambuffer_recorder_ng/
│   ├── camera_control/
│   ├── triggerbox_repository/
│   └── treadmill_repository/
├── build/
├── install/
└── log/
```

Each repository remains an independent Git repository under `src/`.

Do not nest these repositories inside the architecture repository.

## 3. Build workflow

Typical package build:

```bash
cd ~/ros2_ws
colcon build --packages-select <package_name>
source install/setup.bash
```

For changes affecting package dependencies or interfaces, rebuild downstream packages as required.

Build behavior should remain conditional where proprietary or optional SDKs are absent.

## 4. Configuration deployment

Configuration files should be version-controlled in the repository that owns them.

Rig profiles should identify:

- Hostnames
- Device aliases
- Camera YAML files
- Optional components
- Launch behavior
- Shutdown behavior

Avoid editing deployed configuration without committing or recording the change.

## 5. Branch and release strategy

Recommended workflow:

- `main` remains usable.
- Feature work occurs on named branches.
- Hardware tests are recorded in commit or pull-request notes.
- Merges use reviewable commits.
- Stable experiment configurations receive tags or releases.
- The exact commit used for important data collection should be recorded with the experiment.

## 6. Deployment verification

After deploying code to a machine:

1. Confirm branch and commit.
2. Build the affected package.
3. Source the current workspace.
4. Check device permissions.
5. Run software-only tests.
6. Run hardware smoke tests.
7. Confirm expected ROS 2 nodes and services.
8. Record any machine-specific deviations.

## 7. Machine-specific setup

Machine-specific settings may include:

- udev rules
- XIMEA SDK installation
- kernel command-line settings
- user group membership
- Chrony configuration
- network route configuration
- ROS domain ID
- middleware selection
- systemd services

These should be scripted or documented rather than relying on memory.
