from golang:alpine as builder

RUN apk update && apk add \
  git

RUN go get -u github.com/golang/protobuf/protoc-gen-go

from alpine

COPY --from=builder /go/bin/protoc-gen-go /usr/bin/protoc-gen-go

RUN apk update && apk add \
  bash \
  protobuf

ENTRYPOINT ["protoc"]
