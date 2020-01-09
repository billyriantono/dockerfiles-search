FROM ros:kinetic-ros-base

LABEL maintainer="maglovato@gmail.com"

WORKDIR /opt

RUN apt-get update
RUN apt-get install -y python-pip
RUN apt-get install -y --reinstall python-rospkg python-rosdep python-catkin-pkg python-rosinstall python-vcstools
RUN apt-get install -y ros-kinetic-tf
RUN apt-get install -y ros-kinetic-tf-conversions
RUN pip install pytest
RUN pip install nose
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN apt-get autoremove -y
RUN apt-get clean

RUN mkdir -p /opt/bin/
ADD start-roscore.sh /opt/bin/start-roscore.sh
