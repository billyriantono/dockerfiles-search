#
# Ubuntu Dockerfile
#

# Pull base image.
FROM ubuntu:14.04

# Install.
RUN \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y byobu curl git vim wget software-properties-common

# Define default command.
CMD ["bash"]
