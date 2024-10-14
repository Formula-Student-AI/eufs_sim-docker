# README

This folder provides .devcontainer files for VSCode to build a Ubuntu 20.04 docker container with ROS 2 Galactic and EUFS sim installed.

## Versions
- OS: Ubuntu 20.04 (Focal)
- ROS: ROS 2 Galactic

## Setup

> **Warning:** eufs_sim-docker currently doesn't run on Apple Silicon (most newer MacBook models) or any computer with an ARM-based CPU. See our [setup guide](https://bristol-fsai.notion.site/Guides-11c29866e62680b3a193ee29496b3f37) to see how to set EUFS sim up in a VM.

0. Follow the [setup guide](https://bristol-fsai.notion.site/Guides-11c29866e62680b3a193ee29496b3f37) if you need to set up Docker.

1. Navigate to your home folder and clone this repo
   ```
   git clone https://github.com/Formula-Student-AI/eufs_sim-docker
   ```

2. Reopen in Container
   - Open the cloned repository in VSCode.
   - Click on the blue box in the bottom left-hand corner of the VSCode window.
   - Select "Reopen in Container".

3. Install ROS Dependencies for EUFS Sim (**this is now optional** - dependencies should be installed in Dockerfile)
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
