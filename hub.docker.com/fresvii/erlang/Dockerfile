FROM alpine:3.4

ENV ERLANG_VERSION 19.0.5

RUN set -ex \
  && apk add --no-cache --virtual .erlang-builddeps \
    autoconf \
    build-base \
    curl \
    ncurses-dev \
    openssl-dev \
  && curl -fSL -o otp.tar.gz "https://github.com/erlang/otp/archive/OTP-$ERLANG_VERSION.tar.gz" \
  && mkdir -p /usr/src \
  && tar -xzf otp.tar.gz -C /usr/src \
  && mv "/usr/src/otp-OTP-$ERLANG_VERSION" /usr/src/otp \
  && rm otp.tar.gz \
  && cd /usr/src/otp \
  && ./otp_build autoconf \
  && ./configure --prefix=/usr \
    --enable-smp-support \
    --enable-threads \
    --enable-m64-build \
    --enable-kernel-poll \
    --enable-hipe \
    --without-javac \
    --enable-dirty-schedulers \
    --enable-sharing-preserving \
  && make -j"$(getconf _NPROCESSORS_ONLN)" \
  && make install \
  && apk add --no-cache --virtual .erlang-rundeps \
    ncurses-dev \
    openssl-dev \
  && apk del .erlang-builddeps \
  && rm -rf \
    /usr/src/otp \
    /var/cache/apk/*
