FROM ubuntu:14.04
MAINTAINER vitr <vitdotonline@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

# Update packages
RUN apt-get update && apt-get install \
    -y --force-yes \
    build-essential \
    git \
    curl \
    python

# Install latest version of pip
RUN curl -O https://bootstrap.pypa.io/get-pip.py && python get-pip.py

# Install AWS CLI
RUN pip install awscli awsebcli

# Set ~/.aws as default dir for bash
RUN echo cd /root/.aws >> ~/.bashrc

# Volumes
VOLUME ["/root/.aws"]

# Make sure we land in a shell
CMD ["/bin/bash"]
