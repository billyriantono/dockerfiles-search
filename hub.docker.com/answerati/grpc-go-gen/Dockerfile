FROM golang:1.10

ENV GRPC_RELEASE_TAG 1.6.0
ENV PROTOBUFF_RELEASE_TAG 3.4.0

RUN go get -u google.golang.org/grpc
RUN go get -u github.com/golang/protobuf/protoc-gen-go

WORKDIR /tmp

RUN apt-get update \
    && apt-get install --yes unzip \
    && rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/google/protobuf/releases/download/v${PROTOBUFF_RELEASE_TAG}/protoc-${PROTOBUFF_RELEASE_TAG}-linux-x86_64.zip \
    && unzip protoc-${PROTOBUFF_RELEASE_TAG}-linux-x86_64.zip -d /opt/protoc

RUN rm -rf /tmp/*

ENV PATH $PATH:/opt/protoc/bin

WORKDIR /usr/src/app

ENTRYPOINT protoc -I. \
    --plugin=protoc-gen-grpc \
    --go_out=plugins=grpc,paths=source_relative:. \
    ${PROTO_FILES}
