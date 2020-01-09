FROM josemrb/debian:stretch-20190228
LABEL maintainer="Jose Miguel Rivero Bruno <work@josemrb.com>"

RUN \
      apt-get update -qq && \
      apt-get install -qq --no-install-recommends \
      autoconf \
      automake \
      build-essential \
      libncurses5-dev \
      libssh-dev \
      m4 \
      unixodbc-dev

RUN adduser --shell /bin/bash --home /build --disabled-password build

RUN echo "%build ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER build
WORKDIR /build

ENV \
  ASDF_DIR=/build/.asdf \
  ASDF_BIN=/build/.asdf/bin \
  ASDF_SHIMS=/build/.asdf/shims
ENV PATH=$ASDF_SHIMS:$ASDF_BIN:$PATH

RUN git clone https://github.com/asdf-vm/asdf.git $ASDF_DIR --branch v0.7.0
