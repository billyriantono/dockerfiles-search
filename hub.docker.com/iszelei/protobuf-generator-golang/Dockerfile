FROM golang:1.12.6

WORKDIR /usr/local

# protoc
RUN apt-get update && apt-get -y install unzip
RUN curl -L -o protoc.tar.gz https://github.com/protocolbuffers/protobuf/releases/download/v3.8.0/protoc-3.8.0-linux-x86_64.zip
RUN unzip protoc.tar.gz

# protoc-gen-go
RUN go get github.com/golang/protobuf/protoc-gen-go

WORKDIR /tmp
ENTRYPOINT ["protoc"]