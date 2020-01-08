FROM alpine:latest
MAINTAINER Enrico Lamperti <elamperti@users.noreply.github.com>

RUN apk add --update make git gcc musl-dev && \
    cd /tmp && \
    git clone -b develop --depth=1 https://github.com/elamperti/mcrcon && \
    cd mcrcon && \
    make && make install && \
    cd - && rm -rf /tmp/mcrcon && \
    apk del make git gcc musl-dev 

ENTRYPOINT ["mcrcon"]
