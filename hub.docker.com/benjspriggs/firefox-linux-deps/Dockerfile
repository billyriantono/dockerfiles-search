FROM rust

LABEL maintainer="ben@sprico.com"

ENV MOZILLA_ARCHIVE tip.tar.gz
ENV MOZILLA_CENTRAL https://hg.mozilla.org/mozilla-central/archive/tip.tar.gz 

# install python, pip, virtualenv
RUN apt-get update
RUN apt-get install -y \
      python-pip \
      libpango1.0-dev \
      unzip \
      zip \
      llvm-3.9 \
      clang-3.9 \
      autoconf2.13 \
      build-essential \
      libgtk-3-dev \
      libgtk2.0-dev \
      libgconf2-dev \
      libdbus-glib-1-dev \
      yasm \
      libpulse-dev \
      && pip install virtualenv

RUN rm -rf /var/cache/apt-get/*

WORKDIR /src

RUN virtualenv .
ADD $MOZILLA_CENTRAL .
RUN tar -xzf $MOZILLA_ARCHIVE && rm $MOZILLA_ARCHIVE
RUN mv mozilla-central-* mozilla-central

# clean up size
RUN apt-get clean
RUN apt-get autoclean
RUN apt-get autoremove

WORKDIR mozilla-central

