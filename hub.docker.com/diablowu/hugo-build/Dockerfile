FROM alpine:3.9

WORKDIR /hugo
ENV HUGO_VERSION=0.61.0

ADD https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz /tmp/
RUN apk add git \
    && cd /tmp && tar -xzvf /tmp/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz \
    && mv /tmp/hugo /usr/local/bin/hugo && chmod +x /usr/local/bin/hugo \
    && rm -f /tmp/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz
