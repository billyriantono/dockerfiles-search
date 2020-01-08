# Ubuntu 12.04 container with en_AU locale support and upgraded udev.

FROM ubuntu-debootstrap:12.04

# Set locale to be en_AU.
RUN locale-gen en_AU en_AU.UTF-8
RUN DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales
RUN update-locale LC_ALL=en_AU.UTF-8 LANG=en_AU.UTF-8 LANGUAGE=en_AU:en

# Setup environment variables
ENV LANG en_AU.UTF-8
ENV LANGUAGE en_AU:en
ENV LC_ALL en_AU.UTF-8

# Upgrade udev here as it's not supported on CircleCI.
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y udev
