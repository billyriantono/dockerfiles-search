FROM ubuntu:14.04

MAINTAINER Chris Daish <chrisdaish@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV uid 1000
ENV gid 1000

RUN useradd -m vlc && \
    apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:videolan/master-daily && \
    apt-get update && \
    apt-get install -y vlc && \
    rm -rf /var/lib/apt/lists/*

COPY start-vlc.sh /tmp/

ENTRYPOINT ["/tmp/start-vlc.sh"]
