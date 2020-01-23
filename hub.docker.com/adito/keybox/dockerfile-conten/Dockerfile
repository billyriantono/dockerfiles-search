FROM debian:latest

MAINTAINER Anton Dieterle <antondie@gmail.com>

# Reduce install footprint
COPY apt-no-recommends.conf /etc/apt/apt.conf.d/no-recommends
COPY dpkg-no-doc.conf /etc/dpkg/dpkg.cfg.d/no-doc

# Base system tools and locale config
RUN apt-get update -qq \
    && apt-get install -y \
      ca-certificates \
      curl \
      git \
      locales \
      wget \
    && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen \
    && rm -rf /var/lib/apt/lists/*

ENV LANG en_US.UTF-8
