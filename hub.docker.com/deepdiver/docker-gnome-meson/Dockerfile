FROM ubuntu:bionic

# Shell
SHELL ["/bin/bash","-c"]

# Get updates install dependencies
RUN apt-get update -qq && \
    apt-get install g++ git python3 python3-setuptools build-essential pkg-config libdbus-1-dev libgirepository1.0-dev libgtk-3-dev libjson-glib-dev libsecret-1-dev libsoup2.4-dev librest-dev libwebkit2gtk-4.0-dev libgcr-3-dev libkrb5-dev valac ninja-build -y && \
    apt-get clean && rm -rf /var/lib/apt/list/*

RUN git clone https://github.com/mesonbuild/meson.git && cd meson && python3 setup.py install


