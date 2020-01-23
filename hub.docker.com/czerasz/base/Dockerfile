# FROM ubuntu:14.04
FROM ubuntu:latest

MAINTAINER Michał Czeraszkiewicz <czerasz.hosting@gmail.com>

# Set the reset cache variable
ENV REFRESHED_AT 2014-11-25

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

# Set locales 
RUN locale-gen en_US en_US.UTF-8 && dpkg-reconfigure locales

# --- SYSTEM UPDATE ---
RUN apt-get update



# --- BASIC PACKAGES ---

# Install basic packages
# apt-get install -y  && ... taken from https://github.com/dockerfile/ubuntu
RUN apt-get install -y build-essential && \
    apt-get install -y software-properties-common && \
    apt-get install -y pwgen \
                       python-software-properties \
                       vim \
                       curl \
                       wget \
                       git \
                       unzip \
                       tree \
                       byobu

# python-software-properties:
# This software provides an abstraction of the used apt repositories. It allows you to easily manage your distribution and independent software vendor software sources.
# Example: It can be used to install nginx from Nginx PPA on Launchpad.

# Additional optional packages:
# - python-setuptools - easy_install
# - software-properties-common - Provides us with add-apt-repository
# - htop
# - iotop
# - net-tools