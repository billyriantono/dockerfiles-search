FROM alpine:latest
MAINTAINER nickg
WORKDIR /tmp
RUN /bin/true \
  && apk update && apk upgrade \
  && apk add nodejs \
  && npm cache clean \
  && rm -rf /var/cache/apk/*
