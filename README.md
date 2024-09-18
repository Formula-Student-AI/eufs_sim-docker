# README

This folder provides .devcontainer files for VSCode to build a Ubuntu 20.04 docker container with ROS 2 Galactic and EUFS sim installed.

## Versions
- OS: Ubuntu 20.04 (Focal)
- ROS: ROS 2 Galactic

## Instructions

> **Warning:** If you're on a MacBook with an M-chip (most newer MacBook models) or any computer with an ARM CPU, you will need to switch to the 'dynamic-os-selection-eufs' branch after cloning the repo (`git switch dynamic-os-selection-eufs`). This is a temporary fix.

0. Download VScode and Docker Desktop. For Windows users: Install WSL (Windows Subsystem for Linux) using `wsl --install` in PowerShell. When you open VSCode you need to click on the blue arrows in the bottom left of the window and then click 'connect to WSL' to open VSCode in Linux ([read more about WSL online](https://www.sitepoint.com/wsl2/) if you're having any trouble with this).

1. Navigate to your home folder and clone this repo
   ```
   git clone https://github.com/Formula-Student-AI/eufs_sim-docker
   ```

2. Reopen in Container
   - Open the cloned repository in VSCode.
   - Click on the blue box in the bottom left-hand corner of the VSCode window.
   - Select "Reopen in Container".

3. Install ROS Dependencies for EUFS Sim (you may need to run this command every time you rebuild or reopen the container to ensure that all necessary dependencies are installed. For some reason, rosdep doesn't like being used in the Dockerfile - we're working on this.)
   ```
   sudo rosdep install --from-paths $EUFS_MASTER --ignore-src -r -y
   ```

4. Build and Install the ROS Packages
   ```
   colcon build --symlink-install
   ```

4. Source the Overlay Setup Script
   ```
   source install/setup.bash
   ```

5. Launch EUFS Sim
   ```
   ros2 launch eufs_launcher eufs_launcher.launch.py
   ```

If you have any problems check [Known Issues with EUFS sim](https://gitlab.com/eufs/eufs_sim/-/wikis/Getting-Started-Guide#4-known-issues-) first. Contact Dan ([ut20461@bristol.ac.uk](mailto:ut20461@bristol.ac.uk)) if you think you've found any bugs.

## Credit
- ijnek: https://github.com/ijnek/ros-devcontainer-template
- EUFS: https://gitlab.com/eufs
