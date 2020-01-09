FROM golang:1.12.4-alpine3.9 as builder

RUN apk add --update --no-cache build-base curl git upx && \
  rm -rf /var/cache/apk/*

RUN GO111MODULE=on go get github.com/micro/protoc-gen-micro && \
    go get -u github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway && \
    go get -u github.com/unistack-org/protoc-gen-microrest && \
    go get -u github.com/favadi/protoc-go-inject-tag && \
    go get -u github.com/envoyproxy/protoc-gen-validate && \
    go get -u github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger

FROM uber/prototool:latest

COPY --from=builder /go/bin/protoc-* /usr/local/bin/