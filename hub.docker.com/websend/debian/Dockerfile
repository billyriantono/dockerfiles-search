# Build: docker build -t websend/debian:8.4-1 .

FROM debian:8.4
MAINTAINER Ilja Krijger <i.krijger@websend.nl>

ENV DEBIAN_FRONTEND noninteractive

RUN \
  apt-get -yq update && \
  apt-get -yq install apt-utils && \
  apt-get -yq upgrade && \
  apt-get install -yq locales && \
  apt-get install -yq build-essential && \
  apt-get -yq install wget unzip git && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  dpkg-reconfigure locales && \
  echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && \
  locale-gen

ENV LANG en_US.utf8
ENV LANGUAGE en_US.utf8
ENV LC_ALL en_US.utf8
