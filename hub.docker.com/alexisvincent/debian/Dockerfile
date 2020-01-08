#
# Debian Dockerfile
#
# https://github.com/alexisvincent/Dockerfiles/debian
#

# Pull base image.
FROM debian:jessie
MAINTAINER Alexis Vincent "alexisjohnvincent@gmail.com"

ENV DEBIAN_FRONTEND noninteractive

# Install.
RUN \
  apt-get update && \
  apt-get install -y git wget supervisor && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["bash"]