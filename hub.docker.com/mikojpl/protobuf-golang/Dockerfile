FROM golang:1.13

LABEL maintainer="mikoj@mynwt.eu"

RUN apt-get update && \
    apt-get -y install unzip && \
    rm -rf /var/lib/apt/lists/* && \
    curl https://github.com/protocolbuffers/protobuf/releases/download/v3.9.2/protoc-3.9.2-linux-x86_64.zip -L -o protobuf.zip && \
    unzip protobuf.zip bin/protoc && \
    chmod +x bin/protoc && \
    rm protobuf.zip

RUN go get -u -v github.com/golang/protobuf/protoc-gen-go
