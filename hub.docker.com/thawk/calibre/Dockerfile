# easily convert ebooks
FROM debian:latest

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/thawk/docker-calibre.git" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.schema-version="1.0.0-rc1"

RUN mkdir /documents
VOLUME ["/documents"]
WORKDIR /documents

ENV PYTHONIOENCODING=utf-8
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8

RUN apt-get update \
&&  apt-get install --no-install-recommends -y \
    calibre \
&&  rm -rf /var/lib/apt/lists/*
