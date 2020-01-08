FROM alpine:3.2

MAINTAINER jsongo <jsongo@qq.com>

ADD . /src
WORKDIR /src

ENV PROTOBUF_TAG v3.3.1

RUN ./build.sh

CMD ["protoc"]
