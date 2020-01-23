FROM debian:jessie

MAINTAINER "Daniel Lucas" <daniel.chris.lucas@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN echo "Europe/Paris" > /etc/timezone; dpkg-reconfigure tzdata && \
    echo "DEBIAN_FRONTEND=noninteractive" >> /etc/environment && \
    echo 'APT::Install-Recommends "0" ; APT::Install-Suggests "0" ;' >> /etc/apt/apt.conf && \
    apt-get update -y && \
    apt-get install -y --no-install-recommends --no-install-suggests \
    adduser \
    sudo && \
    adduser --disabled-password --gecos '' developer && \
    adduser developer sudo && \
    adduser developer staff && \
    usermod -g staff developer && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    apt-get clean -y && \
    rm -rf /lib/xtables/libip6*

USER developer
