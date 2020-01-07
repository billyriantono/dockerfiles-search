FROM isaackuang/alpine-base:3.8.0

RUN echo "http://dl-3.alpinelinux.org/alpine/edge/main" >> /etc/apk/repository && \
    echo "http://dl-3.alpinelinux.org/alpine/edge/community" >> /etc/apk/repository && \
    apk --no-cache --progress add musl-dev git go && \
    mkdir /go

ENV GOPATH=/go \
    GOBIN=/go/bin
