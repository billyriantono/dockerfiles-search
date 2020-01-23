FROM alpine:latest

LABEL maintainer="Anthony Porthouse <anthony@porthou.se>"

RUN apk add --no-cache \
    ca-certificates \
    curl \
    tar

ENV HUGO_VERSION 0.35

RUN curl -LO https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz \
    && tar zxf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz \
    && mv hugo /usr/local/bin/hugo \
    && rm hugo_${HUGO_VERSION}_Linux-64bit.tar.gz

EXPOSE 1313

ENTRYPOINT ["hugo"]

WORKDIR /opt