FROM osrf/ros:galactic-desktop

# Add vscode user with same UID and GID as your host system
# (copied from https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_creating-a-nonroot-user)
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
# Switch from root to user
USER $USERNAME

# Add user to video group to allow access to webcam
RUN sudo usermod --append --groups video $USERNAME

# Install Git
RUN sudo apt install -y git

# Rosdep update
RUN rosdep update

# Update all packages
RUN sudo apt update && sudo apt upgrade -y

## Trying to figure out how to install rosdep dependencies during build
# SHELL ["/bin/bash", "-c"]
# ARG WORKSPACE_DIR=/eufs-sim
# RUN ls -la $(pwd)
# RUN source /opt/ros/${ROS_DISTRO}/setup.bash \
#     && sudo rosdep install --from-paths /eufs-sim --ignore-src -r -y

# Additional dependency to fix zed camera not showing up in rviz
RUN sudo apt install -y python3-tk

# Source the ROS setup file
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc
