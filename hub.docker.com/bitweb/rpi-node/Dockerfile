FROM resin/armv7hf-debian-qemu
MAINTAINER Tõnis Tobre <tobre@bitweb.ee>

ENV DEBIAN_FRONTEND noninteractive

RUN [ "cross-build-start" ]

RUN apt-get update && \
    apt-get install -yq \
            apt-transport-https \
            curl

RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -
RUN echo 'deb https://deb.nodesource.com/node_6.x jessie main' > /etc/apt/sources.list.d/nodesource.list
RUN echo 'deb-src https://deb.nodesource.com/node_6.x jessie main' >> /etc/apt/sources.list.d/nodesource.list

RUN apt-get update && \
    apt-get install -yq \
            nodejs

RUN [ "cross-build-end" ]
