FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade -y && \
        apt-get install -y xterm aptitude tmux nano bash sudo dnsutils openssh-client iputils-ping && \
        apt-get clean

RUN groupadd --gid 1000 user && \
        useradd --uid 1000 --gid 1000 --create-home --shell /bin/bash user

RUN echo "user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

