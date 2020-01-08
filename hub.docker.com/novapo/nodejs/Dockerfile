FROM novapo/alpine:edge
MAINTAINER Philip Graf <mail@philipgraf.de>

VOLUME ["/app"]

WORKDIR /app
CMD ["bash"]

RUN apk update && \
  apk add \
    build-base \
    git \
    nodejs-dev \
    nodejs && \
  rm -rf /var/cache/apk/*

ADD rootfs /
