## Ubuntu base image ##
#  dockering/ubuntu
#
## https://github.com/andyvl/dockering ##

FROM ubuntu:14.04

# Install updates and commonly used utils.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y wget curl git unzip vim && \
  rm -rf /var/lib/apt/lists/*

# Define default command.
CMD ["bash"]
