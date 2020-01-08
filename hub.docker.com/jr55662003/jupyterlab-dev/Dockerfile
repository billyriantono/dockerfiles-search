FROM ubuntu:16.04

LABEL maintainer="HaoChun Chang <changhaochun84@gmail.com>"

# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Update the apt-get and installs curl
RUN apt-get update \
  && apt-get install -y curl

# Installs node.js, python, pip and setup tools
RUN apt-get install -y \
    python3 \
    python3-pip \
    python3-setuptools \
    python3-tk \
    nodejs-legacy \
    build-essential \
    libzmq3-dev \
    npm

# Upgrade pip
RUN pip3 install --upgrade pip

# Install jupyter notebook
RUN pip3 install \
  jupyter \
  jupyterlab

# Fix ipython kernel version
RUN ipython3 kernel install

RUN npm install -g ijavascript
RUN ijsinstall
