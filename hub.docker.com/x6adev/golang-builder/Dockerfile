FROM golang:latest

LABEL "com.github.actions.name"="Golang Builder"
LABEL "com.github.actions.description"="x6a golang builder"

ENV TERM xterm-256color

ENV PROTOC_VERSION 3.11.2
RUN apt-get -y update && apt-get -y install unzip docker.io && \
    curl -sSL --retry 3 --retry-connrefused https://taskfile.dev/install.sh | sh -s -- -b /usr/local/bin && \
    curl -sSL --retry 3 --retry-connrefused https://install.goreleaser.com/github.com/goreleaser/goreleaser.sh | sh -s -- -b /usr/local/bin && \
    curl -sSL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b /usr/local/bin && \
    mkdir -p /tmp/protoc && \
    curl -sLo /tmp/protoc/protoc.zip --retry 3 --retry-connrefused https://github.com/protocolbuffers/protobuf/releases/download/v${PROTOC_VERSION}/protoc-${PROTOC_VERSION}-linux-x86_64.zip && \
    unzip -q /tmp/protoc/protoc.zip -d /tmp/protoc && \
    mv /tmp/protoc/bin/protoc /usr/local/bin/protoc && \
    chmod +x /usr/local/bin/protoc && \
    rm -rf /tmp/protoc && \
    go get -u \
        github.com/golang/protobuf/proto \
        github.com/golang/protobuf/protoc-gen-go \
        github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway \
        github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger \
        github.com/kisielk/errcheck \
        golang.org/x/tools/cmd/goimports \
        golang.org/x/lint/golint \
        github.com/securego/gosec/cmd/gosec \
        golang.org/x/tools/go/analysis/passes/shadow/cmd/shadow \
        honnef.co/go/tools/cmd/staticcheck

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
