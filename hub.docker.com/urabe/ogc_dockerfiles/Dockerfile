# Firos2

FROM      ubuntu:16.04
MAINTAINER Kazuki Urabe <urabe.kazuki@tis.co.jp>

# ROS2 install
RUN apt update
RUN apt install -y curl
RUN curl http://repo.ros2.org/repos.key | apt-key add -
RUN sh -c 'echo "deb [arch=amd64,arm64] http://repo.ros2.org/ubuntu/main xenial main" > /etc/apt/sources.list.d/ros2-latest.list'

RUN apt update
RUN apt install locales
RUN locale-gen en_US en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
RUN export LANG=en_US.UTF-8
RUN apt install -y `apt list "ros-ardent-*" 2> /dev/null | grep "/" | awk -F/ '{print $1}' | grep -v -e ros-ardent-ros1-bridge -e ros-ardent-turtlebot2- | tr "\n" " "`

# RUN source /opt/ros/ardent/setup.bash

# Firos2 install
RUN apt install -y git wget
RUN apt install -y build-essential cppcheck cmake libopencv-dev python-empy python3-dev python3-empy python3-nose python3-pip python3-pyparsing python3-setuptools python3-vcstool python3-yaml libtinyxml-dev libeigen3-dev
RUN apt install -y clang-format pydocstyle pyflakes python3-coverage python3-mock python3-pep8 uncrustify
RUN pip3 install argcomplete
RUN pip3 install flake8 flake8-blind-except flake8-builtins flake8-class-newline flake8-comprehensions flake8-deprecated flake8-docstrings flake8-import-order flake8-quotes pytest pytest-cov pytest-runner
RUN apt install -y libasio-dev libtinyxml2-dev

RUN mkdir -p ~/ros2_ws/src
RUN cd ~/ros2_ws
RUN wget https://raw.githubusercontent.com/ros2/ros2/master/ros2.repos
RUN vcs import ~/ros2_ws/src < ros2.repos

RUN cd ~/ros2_ws/src/ros2
RUN git clone --recursive https://github.com/eProsima/firos2
# RUN ament build --only-package firos2
