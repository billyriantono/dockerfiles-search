# Pull base image.
FROM ubuntu:16.04

MAINTAINER Cristi DRAGHICI <cristi@draghici.net>

# Install.
RUN \
  apt-get update && \
  apt-get install -y git && \
  cd /root && \
  git clone https://github.com/cristidraghici/bash.git

RUN \
  chmod +x /root/bash/run.sh

# Set volume
ADD . /root
VOLUME ["/root"]

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["bash"]

# Expose apache port
EXPOSE 80
EXPOSE 3306
