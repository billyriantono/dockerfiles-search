FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y unzip wget golang git

RUN wget -q https://github.com/protocolbuffers/protobuf/releases/download/v3.9.0/protoc-3.9.0-linux-x86_64.zip -O protoc.zip && \
    unzip protoc.zip -d /usr && \
    rm protoc.zip

RUN go get -u github.com/golang/protobuf/protoc-gen-go

ENV PATH=$PATH:/root/go/bin/

ENTRYPOINT [ "protoc" ]