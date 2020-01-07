FROM golang:1.9.2-alpine

RUN apk add --no-cache git bzr make protobuf
RUN go get github.com/golang/mock/mockgen && \
    go get github.com/golang/protobuf/protoc-gen-go && \
    go get github.com/dominikznidar/govendor && \
    go get github.com/go-swagger/go-swagger/cmd/swagger
