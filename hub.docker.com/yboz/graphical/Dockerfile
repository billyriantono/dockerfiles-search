FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && apt-get install -y \
    pkg-config \
    dbus \
    dbus-x11 \
    wget \
    netcat \
    iputils-ping \
    git \
    libxi6 \
    libgcc1 \
    libfreetype6 \
    libxrender1 \
    libdbus-c++ \
    libxtst6 \
    libgtk-3-0 \
    libxss1 \
    libgconf2-4 \
    libnss3 \
    libcanberra-gtk-module \
    libasound2 && \
    useradd -ms /bin/bash dev
