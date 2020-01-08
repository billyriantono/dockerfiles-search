FROM kalilinux/kali-linux-docker:latest

LABEL maintainer="steven@z7ev3n.com"

ENV PACKAGES \
    ansible \
    curl \
    git \
    sudo \
    unzip

RUN apt-get -qq update && \
    apt-get -qq install --fix-missing && \
    DEBIAN_FRONTEND=noninteractive apt-get -qq install -y ${PACKAGES} && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /etc/ansible && \
    echo 'localhost ansible_connection=local' > /etc/ansible/hosts
