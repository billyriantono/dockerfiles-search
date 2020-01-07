FROM ubuntu:xenial

ENV TZ="America/Denver" \
    LANG="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    LANGUAGE="en_US.UTF-8"

ARG DEBIAN_FRONTEND="noninteractive"

RUN apt-get update \
 && apt-get dist-upgrade --yes \
 && apt-get install --yes --no-install-recommends \
    ca-certificates \
    locales \
    tzdata \
 && locale-gen en_US.UTF-8 \
 && apt-get autoremove --yes --purge \
 && apt-get clean \
 && rm --recursive --force /var/lib/apt/lists/* /tmp/* /var/tmp/*
