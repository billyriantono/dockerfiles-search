FROM gcr.io/gcpug-container/appengine-go:latest

ARG PROTOC_VERSION=3.6.1
ARG PROTOTOOL_VERSION=1.3.0

RUN	curl -fo protoc.zip -sSL "https://github.com/google/protobuf/releases/download/v${PROTOC_VERSION}/protoc-${PROTOC_VERSION}-linux-x86_64.zip" && \
	mkdir protoc && \
    unzip -q protoc.zip -d protoc && \
    cp ./protoc/bin/protoc /usr/local/bin/ && \
    cp -rf ./protoc/include/google /usr/local/include/ && \
    rm protoc.zip protoc -rf && \
    go get -u github.com/golang/protobuf/protoc-gen-go && \
    go get -u github.com/favadi/protoc-go-inject-tag && \
    go get -u github.com/golang/dep/cmd/dep && \
    go get -u honnef.co/go/tools/cmd/staticcheck && \
    go get -u golang.org/x/lint/golint && \
    go get -u golang.org/x/tools/cmd/goimports && \
    go get -u mvdan.cc/sh/cmd/shfmt && \
    rm -rf ${GOPATH}/src/github.com/golang ${GOPATH}/pkg && \
    curl -sSL https://github.com/uber/prototool/releases/download/v${PROTOTOOL_VERSION}/prototool-$(uname -s)-$(uname -m)  -o /usr/local/bin/prototool && chmod +x /usr/local/bin/prototool && \
    \
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    \
	apt-get update && \
	apt-get install -yqq --no-install-suggests --no-install-recommends \
		npm \
		dnsutils && \
    rm -rf /var/lib/apt/lists/*

