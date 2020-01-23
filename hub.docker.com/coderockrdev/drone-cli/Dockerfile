FROM golang:1.8.3-alpine3.6
RUN apk update \
    && apk add curl \
    && curl -L https://github.com/drone/drone-cli/releases/download/v0.8.5/drone_linux_amd64.tar.gz | tar zx \
    && install -t /usr/local/bin drone \
    && apk del curl