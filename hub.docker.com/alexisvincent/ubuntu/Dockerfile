#
# Ubuntu Dockerfile
#
# https://github.com/alexisvincent/docker-ubuntu
#

# Pull base image.
FROM ubuntu:14.04

MAINTAINER Alexis Vincent "alexisjohnvincent@gmail.com"

# Install.
RUN \
  apt-get update && \
  apt-get install -y git wget && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["bash"]