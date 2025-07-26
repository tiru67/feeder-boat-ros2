FROM ubuntu:22.04

# Set environment variables for non-interactive apt
ENV DEBIAN_FRONTEND=noninteractive

# Basic setup
RUN apt-get update && apt-get install -y \
    locales curl gnupg2 lsb-release sudo bash-completion git \
    && locale-gen en_US en_US.UTF-8 && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

# ROS 2 Humble setup
RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository universe

# Add ROS 2 key and sources
RUN curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -
RUN sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2.list'

# Install ROS 2 Humble
RUN apt-get update && apt-get install -y \
    ros-humble-desktop \
    python3-colcon-common-extensions \
    && rm -rf /var/lib/apt/lists/*

# Source ROS setup script
SHELL ["/bin/bash", "-c"]
RUN echo "source /opt/ros/humble/setup.bash" >> /home/vscode/.bashrc

# Create user
RUN useradd -ms /bin/bash vscode && adduser vscode sudo
