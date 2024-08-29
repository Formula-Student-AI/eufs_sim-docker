# README

This folder provides .devcontainer files for VSCode to build a Ubuntu 20.04 docker container with ROS 2 Galactic and EUFS sim installed.

## Versions
- OS: Ubuntu 20.04 (Focal)
- ROS: ROS 2 Galactic

## Instructions

0. Download VScode and Docker Desktop

1. Clone this Repo
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

## Credit
- ijnek: https://github.com/ijnek/ros-devcontainer-template
- EUFS: https://gitlab.com/eufs
