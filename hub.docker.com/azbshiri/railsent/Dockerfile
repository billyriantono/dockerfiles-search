FROM kalilinux/kali-rolling:latest

LABEL maintainer="aymericmayeux@gmail.com"

ENV DEBIAN_FRONTEND noninteractive

# Separate command to use layer caching when possible as kali-linux-full is a huge metapackage
RUN apt-get update \
    && apt-get dist-upgrade -y \
    && apt-get install -y kali-linux-full

RUN apt-get install -y \
        network-manager \
        pciutils \
    && apt-get autoremove \
    && apt-get clean \
    && updatedb