FROM alpine:latest
MAINTAINER Yogendra Rampuria <yogendrarampuria@gmail.com>

ENV HUGO_VERSION=0.25.1
ADD https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz /tmp
RUN tar -xf /tmp/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz -C /tmp \
    && mkdir -p /usr/local/sbin \
    && mv /tmp/hugo /usr/local/sbin/hugo \
    && rm -rf /tmp/hugo_${HUGO_VERSION}_linux_amd64

RUN apk update \
    && apk upgrade \
    && apk add --no-cache ca-certificates

VOLUME /app
WORKDIR /app

ENTRYPOINT ["/usr/local/sbin/hugo", "-s", "/app" ]
