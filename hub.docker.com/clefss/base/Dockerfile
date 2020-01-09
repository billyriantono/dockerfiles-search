FROM ubuntu:bionic

LABEL maintainer "clefss <clefss@protonmail.com>"

ENV DEBIAN_FRONTEND=noninteractive \
    TERM=xterm

# Updates
RUN apt-get -qq update &&\
    apt-get -qq upgrade

# Clean up
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get autoremove -y && \
    apt-get clean
