FROM golang:1.11-alpine as build
MAINTAINER dev <aet> fedux dot org

RUN apk update \
    && apk upgrade \
    && apk add git gcc make g++

COPY . /build/local_webserver
WORKDIR /build/local_webserver
RUN bin/build

####

FROM alpine:3.8

RUN apk update --no-cache \
    && apk upgrade --no-cache \
    && apk add tini

COPY --from=build /build/local_webserver/local_webserver /usr/local/bin/local_webserver
RUN chmod +x /usr/local/bin/local_webserver

EXPOSE 80

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/usr/local/bin/local_webserver", "--interface=0.0.0.0", "--port=80", "--directory=/data"]
