FROM        ros:melodic
MAINTAINER  Jason Wang

# set environment variables
ENV         DEBIAN_FRONTEND=noninteractive
ENV         APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

# Install apt-fast and apt-utils
RUN         apt-get update && \
            apt-get install -y --no-install-recommends apt-utils && \
            apt-get install -y --no-install-recommends software-properties-common && \
            add-apt-repository ppa:apt-fast/stable -y && \
            apt-get update && \
            apt-get install -y --no-install-recommends apt-fast

# Add PPA repositories repositories
RUN         apt-get update && apt-fast install -q -y curl && \
            curl -sL https://deb.nodesource.com/setup_10.x | bash && \
            curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash && \
            curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
            add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"


## Installs
RUN         apt-get update && \
            apt-fast -y install  \
            ca-certificates \
            curl \
            gnupg2 \
            unzip \
            ssh \
            docker-ce

## Docker compose
RUN         curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
            chmod +x /usr/local/bin/docker-compose

## ROS dependencies and linter tools
RUN         apt-fast install -y --no-install-recommends \
            python-catkin-tools \
            python-pip \
            git-lfs \
            apt-transport-https \
            flake8 \
            cppcheck

## Set up link to ssh-key
ENV         BITBUCKET_HASH_KEY "2048 97:8c:1b:f2:6f:14:6b:5c:3b:ec:aa:46:46:74:7c:40"
RUN         mkdir /root/.ssh && touch /root/.ssh/known_hosts && \
            ssh-keyscan -H bitbucket.org >> /root/.ssh/known_hosts && \
            ssh-keyscan -H github.com >> /root/.ssh/known_hosts && \
            ssh-keygen -l -f /root/.ssh/known_hosts

# Add tools
ADD         . /usr/local

# Save time by using rosdep install -i --simulate --reinstall --from-paths .
RUN         apt-fast install --no-install-recommends -y \
            supervisor \
            libeigen3-dev \
            nodejs \
            nmap \
            libtinyxml2-dev \
            qtbase5-dev \
            udev \
            libsdl1.2-dev \
            libftdi-dev \
            setserial \
            libpcl-dev \
            libcurl4-openssl-dev \
            curl \
            libjsoncpp-dev \
            python-paramiko \
            python-kombu \
            python-jinja2 \
            python-yaml \
            python-six \
            docker-compose \
            libqt4-dev \
            openssh-server \
            libgtest-dev \
            chromium-browser \
            libyaml-cpp-dev \
            python3-pip \
            python-pbr \
            libboost-all-dev \
            libqt5core5a \
            liblua5.1-0-dev \
            libqt5widgets5 \
            python-mock \
            python-funcsigs \
            python-dev \
            python-scp \
            screen \
            lighttpd \
            python-rospkg \
            libopencv-dev \
            libcpprest-dev \
            libncurses5-dev \
            google-mock \
            golang-go \
            python-flask \
            libpcl-dev \
            iputils-ping \
            postgresql \
            postgresql-contrib \
            gamin \
            libbullet-dev \
            libsdl2-dev \
            libogre-1.9-dev \
            python-enum34 \
            openssl \
            libsdl-image1.2-dev \
            libqt5gui5 \
            unclutter \
            python-concurrent.futures \
            libsdl2-mixer-dev \
            libevdev-dev

## Install ros2
RUN         apt-get update && apt-fast install -y --no-install-recommends curl gnupg2 lsb-release && \
            curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - && \
            sh -c 'echo "deb [arch=amd64] http://packages.ros.org/ros2/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list'
RUN         apt-get update && apt-fast install -y --no-install-recommends ros-dashing-rclcpp
# Developer tools not needed for CI by reduces time on actual build
RUN         apt-fast install -y --no-install-recommends ros-dashing-ros2cli ros-dashing-ros2topic ros-dashing-ros2node ros-dashing-ros2run ros-dashing-ros2service

## Sudo user
RUN         apt-get update && apt-fast install --no-install-recommends -y sudo
RUN         groupadd -g 1000 jenkins \
            && useradd -u 1000 -g 1000 -mrs /bin/bash -b /home -p $(openssl passwd -1 airborne) jenkins \
            && usermod -aG sudo jenkins \
            && echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
USER        jenkins