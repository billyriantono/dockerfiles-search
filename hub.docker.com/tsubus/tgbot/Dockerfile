FROM lsiobase/alpine:3.10

ARG VERSION="1.3"
ARG DATE="2019/11/08"
LABEL build_version="tgbot version:- ${VERSION}, ${DATE}"
LABEL maintainer="tsubus"

# set environment variables
ENV HOME="/config/tgbot"
ENV PGROOT=/config/tgbot/postgres

# volume
VOLUME /config

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

# install ca-certificates so that HTTPS works consistently
# other runtime dependencies for Python are installed later
RUN apk add --no-cache ca-certificates

# install packages
RUN \
 echo "**** install packages ****" && \
 apk update && \
 apk add --no-cache \
    python3-dev \
    git \
    screen \
    postgresql \
    postgresql-dev \
    py3-pip \
    gcc \
    libffi-dev \
    py3-cffi \
    musl-dev \
    py3-pillow && \
 /usr/bin/pip3 install --upgrade pip && \
 git clone https://gitlab.com/tylagat/tgbot.git /app/tgbot && \
 cd /app/tgbot && \
 /usr/bin/pip3 install -r requirements.txt && \
 echo "**** cleanup ****" && \
 rm -rf \
    /root/.cache \
    /tmp/*

# add local files
COPY root/ /
