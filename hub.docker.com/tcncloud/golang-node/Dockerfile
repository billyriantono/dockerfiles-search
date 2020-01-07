FROM golang:1.12

RUN apt update && apt install -y unzip xz-utils

ENV PROTO_VERSION 3.6.1
RUN wget https://github.com/protocolbuffers/protobuf/releases/download/v${PROTO_VERSION}/protoc-${PROTO_VERSION}-linux-x86_64.zip && \
  unzip protoc-${PROTO_VERSION}-linux-x86_64.zip -d /usr/local && \
  rm protoc-*

RUN go get -u github.com/golang/protobuf/protoc-gen-go

ENV NODE_VERSION 10.15.3
RUN wget https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.xz && \
  tar xf node-v${NODE_VERSION}-linux-x64.tar.xz -C /usr/local --strip-component=1 && \
  rm node-* && npm install -g yarn
