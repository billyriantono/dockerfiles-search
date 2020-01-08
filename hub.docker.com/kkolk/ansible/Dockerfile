#
# Ubuntu Dockerfile
#
# https://github.com/dockerfile/ubuntu
#

# Pull base image.
FROM jrei/systemd-ubuntu:16.04

# Install.
RUN \
  apt-get update && \
  apt-get install -y sudo software-properties-common apt-transport-https && \
  apt-add-repository -y ppa:ansible/ansible && \
  add-apt-repository universe && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y ansible python3-yaml python3 python3-paramiko python3-jinja2 && \
rm -rf /var/lib/apt/lists/*
