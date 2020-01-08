FROM ubuntu:14.04

LABEL maintainer="zdm <zdm@softvisio.net>"

USER root

ADD https://download-hr.utorrent.com/track/beta/endpoint/utserver/os/linux-x64-ubuntu-13-04 /var/local/utserver/utserver.tgz

ADD utserver.conf /var/local/utserver

WORKDIR /var/local/utserver

SHELL [ "/bin/bash", "-l", "-c" ]

RUN \
    apt-get update \
    && apt-get -y upgrade \
    && apt-get -y install libssl0.9.8 ca-certificates \
    && apt-get clean \
    \
    && tar --strip-components=1 -xzf utserver.tgz \
    && rm -f utserver.tgz \
    && chmod +x utserver \
    && mkdir settings

ENTRYPOINT [ "/var/local/utserver/utserver", "-configfile", "/var/local/utserver/utserver.conf", "-settingspath", "/var/local/utserver/settings" ]
