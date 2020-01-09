FROM lsiobase/ubuntu:bionic

LABEL maintainer="Christopher Viel <viel.christopher@gmail.com>"

# environment variables
ARG APP_VERSION=0.95.4
ARG DEBIAN_FRONTEND="noninteractive"
ARG INSTALL_LIBCEC="no"

# install software
WORKDIR /app

RUN \
  echo "**** install packages ****" && \
  apt-get update && \
  apt-get install -y \
    autoconf \
    curl \
    gnupg \
    python3 \
    python3-pip \
    wget && \
  pip3 install --no-cache-dir \
    uvloop==0.12.2 \
    cchardet \
    cython && \
  ln -s /usr/bin/python3 /usr/bin/python && \
  ln -s /usr/bin/pip3 /usr/bin/pip && \
  echo "**** download application ****" && \
  wget https://github.com/home-assistant/home-assistant/archive/${APP_VERSION}.tar.gz -O - | tar --strip-components=1 -xz && \
  echo "**** install application ****" && \
  sed -i 's/libsodium18/libsodium23/' virtualization/Docker/setup_docker_prereqs && \
  sed -i -- 's/\/usr\/src\/app\//\/app\//g' virtualization/Docker/scripts/* && \
  virtualization/Docker/setup_docker_prereqs && \
  pip3 install --no-cache-dir -r \
    requirements_all.txt && \
  echo "**** cleanup ****" && \
  rm -rf \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/*

COPY root/ /

ENV PIP_USER=1 \
    PYTHONPATH=/app \
    PYTHONUSERBASE=/python.local

EXPOSE 8123 8300 51827
VOLUME /config /python.local

