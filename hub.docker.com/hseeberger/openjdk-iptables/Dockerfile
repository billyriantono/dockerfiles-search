#
# Dockerfile of iptables on top of OpenJDK
#
# https://github.com/hseeberger/openjdk-iptables
#

# Pull base image
FROM openjdk:8u181

# Install
RUN \
  apt-get update && \
  apt-get install -y iptables

# Define working directory
WORKDIR /root
