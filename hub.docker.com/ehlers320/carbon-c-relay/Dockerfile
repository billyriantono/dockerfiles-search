FROM alpine:3.9 as builder

MAINTAINER Tim Ehlers <ehlerst@gmail.com>

RUN apk --no-cache update

RUN apk --no-cache upgrade

RUN apk --no-cache add git bc build-base curl lz4-dev zlib-dev openssl-dev

RUN mkdir -p /opt/carbon-c-relay-build

RUN mkdir /etc/carbon-c-relay

COPY . /opt/carbon-c-relay-build

RUN \
  cd /opt/carbon-c-relay-build && \
  ./configure; make 

FROM alpine:3.9 

RUN apk add lz4-libs zlib openssl --no-cache

COPY --from=builder /opt/carbon-c-relay-build/relay /usr/bin/carbon-c-relay

EXPOSE 2003

ENTRYPOINT ["carbon-c-relay", "-f", "/etc/carbon-c-relay/carbon-c-relay.conf"]

