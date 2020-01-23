FROM php:cli-alpine

ENV GRPC_VERSION=1.15.0

RUN mkdir -p /data /opt && \
    apk update && \
    apk add protobuf git autoconf automake libtool curl make g++ unzip && \
    mkdir -p /tmp && cd /tmp && git clone --depth=1 -b v${GRPC_VERSION} https://github.com/grpc/grpc && \
    cd grpc && git submodule update --init && make grpc_php_plugin && \
    cp /tmp/grpc/bins/opt/grpc_php_plugin /opt/grpc_php_plugin && \
    rm -rf /tmp/grpc

WORKDIR /data

ENTRYPOINT ["protoc", "--plugin=protoc-gen-grpc=/opt/grpc_php_plugin"]
