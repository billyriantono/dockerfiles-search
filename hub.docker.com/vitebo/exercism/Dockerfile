FROM alpine:3.7

RUN \
  apk add wget tar \
  && wget https://github.com/exercism/cli/releases/download/v3.0.13/exercism-linux-64bit.tgz \
  && tar -xf exercism-linux-64bit.tgz \
  && mv exercism /usr/bin \
  && rm exercism-linux-64bit.tgz

WORKDIR /home/exercism
