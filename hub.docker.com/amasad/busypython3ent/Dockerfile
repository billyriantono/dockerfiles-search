FROM alpine:3.6

MAINTAINER Yoshihisa AMAKATA <amakata@gmail.com>

RUN apk add --no-cache --virtual=pandoc-deps wget ca-certificates && \
    wget https://gitlab.com/ConorIA/alpine-pandoc/raw/master/conor@conr.ca-584aeee5.rsa.pub -O /etc/apk/keys/conor@conr.ca-584aeee5.rsa.pub && \
    echo https://conoria.gitlab.io/alpine-pandoc/ >> /etc/apk/repositories && \
    apk add --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing cmark && \
    apk add --no-cache git bash pandoc jq curl zip && \
    apk del pandoc-deps

WORKDIR /data

ENTRYPOINT ["/usr/bin/pandoc"]

CMD ["--help"]
