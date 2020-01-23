FROM ubuntu:14.04

MAINTAINER Andrey Kanevsky

RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y x11vnc xvfb firefox && \
    mkdir ~/.vnc && \
    touch ~/.vnc/passwd

RUN x11vnc -storepasswd "devopsil" ~/.vnc/passwd

RUN sh -c 'echo "firefox" >> ~/.bashrc'

CMD ["/usr/bin/x11vnc", "-forever", "-usepw", "-create"]
