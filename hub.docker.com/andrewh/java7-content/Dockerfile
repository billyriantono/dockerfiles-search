# -*- coding: utf-8 -*-
#
# =============================================================================
#
# Made with a template from:
#   https://www.github.com/andrerichter/docker-volume-permission-template
#
# Author(s):
#   Andre Richter, <andre.o.richter@gmail.com>
#
# =============================================================================
FROM ubuntu:16.04

MAINTAINER Andre Richter <andre.o.richter@gmail.com>

ARG IMAGE_NAME
ENV IMAGE_NAME=$IMAGE_NAME

ARG DEBIAN_FRONTEND=noninteractive
ENV TERM=xterm-256color

RUN set -ex;                                      \
    tempPkgs='                                    \
        ca-certificates                           \
        wget                                      \
        unzip                                     \
    ';                                            \
    apt-get update;                               \
    apt-get install -q -y --no-install-recommends \
        $tempPkgs;                                \
    # Do something with tempPkgs
    wget https://www.phidgets.com/downloads/phidget22/libraries/linux/libphidget22.tar.gz; \
    wget https://www.phidgets.com/downloads/phidget22/libraries/any/Phidget22Python.zip;   \
    unzip Phidget22Python.zip;                    \
    # Cleanup tempPkgs
    apt-get purge -y --auto-remove $tempPkgs;     \
    # Install persistend packages
    apt-get update;                               \
    apt-get install -q -y --no-install-recommends \
        build-essential                           \
        usbutils                                  \
        libusb-1.0-0-dev                          \
        python                                    \
        ;                                         \
    apt-get autoremove -q -y;                     \
    apt-get clean -q -y;                          \
    rm -rf /var/lib/apt/lists/*;                  \
    tar -xzf libphidget22.tar.gz;                 \
    cd libphidget22*;                             \
    ./configure --prefix=/usr;                    \
    make;                                         \
    make install;                                 \
    cd ../Phidget22Python;                        \
    python setup.py install;                      \
    cd ..;                                        \
    rm -rf libphidget22* Phidget22Python*
