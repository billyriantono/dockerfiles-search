FROM amd64/node:10-alpine

RUN apk add python make git \
  && mkdir -p /opt/staging && cd /opt \
  && wget -O - https://musl.cc/arm-linux-musleabihf-cross.tgz | tar -xz \
  && ls /opt

ENV CC=/opt/arm-linux-musleabihf-cross/bin/arm-linux-musleabihf-gcc \
    CXX=/opt/arm-linux-musleabihf-cross/bin/arm-linux-musleabihf-g++ \
    STAGING_DIR=/opt/staging
