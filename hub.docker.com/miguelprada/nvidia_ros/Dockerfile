FROM miguelprada/nvidia_ros:kinetic

RUN apt-get update -qq \
    && apt-get -qq install --no-install-recommends -y \
        ros-$ROS_DISTRO-desktop \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
