FROM alpine:3.4

COPY ./pubkeys/ /etc/apk/keys/

RUN echo '@edge http://dl-cdn.alpinelinux.org/alpine/edge/main' \
  >> /etc/apk/repositories \
  && echo 'http://dl-cdn.alpinelinux.org/alpine/edge/community' \
  >> /etc/apk/repositories \
  && echo 'http://dl-cdn.alpinelinux.org/alpine/edge/testing' \
  >> /etc/apk/repositories \
  && echo '@meteogrid https://s3-eu-west-1.amazonaws.com/meteogrid-apk/' \
  >> /etc/apk/repositories
