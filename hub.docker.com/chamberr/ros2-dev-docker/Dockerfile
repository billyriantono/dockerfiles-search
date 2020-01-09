FROM ubuntu:18.04

# Enable udevd
ENV UDEV=1

# Set non-interractive
ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
	build-essential \
	byobu \
	curl \
	gnupg2 \
	locales \
	mercurial \
	nano \
	python3 \
	python3-argcomplete \
	python3-dev \
	python3-pip \
	vim

# Set the locale
RUN locale-gen en_US en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG en_US.UTF-8

# Authorize gpg key
RUN curl http://repo.ros2.org/repos.key | apt-key add -

RUN /bin/bash -c 'echo "deb [arch=amd64,arm64] http://packages.ros.org/ros2/ubuntu bionic main" > /etc/apt/sources.list.d/ros2-latest.list'

# Install ROS2 Dashing
RUN apt-get update && apt-get install -y --no-install-recommends \
	ros-dashing-ros-base \
	&& rm -rf /var/lib/apt/lists/*

# install python packages
COPY ./requirements.txt /requirements.txt
RUN pip3 install wheel
RUN pip3 install -r /requirements.txt

# Start
CMD ["bash", "/app/start.sh"]
