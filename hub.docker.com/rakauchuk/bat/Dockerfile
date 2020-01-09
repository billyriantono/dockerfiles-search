FROM alpine:3.10

ENV BAT_VERSION 0.12.1-r1
ENV BASH_VERSION 5.0.0-r0

RUN set -x \
    && apk add bash=${BASH_VERSION} \
    && apk add bat=${BAT_VERSION} --update-cache -X http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted \
    && echo "shopt -s checkwinsize" >> ~/.bashrc

WORKDIR /app

ENTRYPOINT [ "bash", "-c", "sleep 0.1; bat $0 $@" ]
