#
# Dockerfile for Yocto environment
#

# Pull base image.
FROM wubicu/lxde-desktop
MAINTAINER Gavin Cho "gavin.cho@wubicu.com"

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y iptables python-gtk2 && \
  apt-get install -y gawk diffstat unzip texinfo gcc-multilib chrpath socat libsdl1.2-dev xterm && \
  rm -rf /var/lib/apt/lists/*

# Define default command.
CMD su -l ${USER}