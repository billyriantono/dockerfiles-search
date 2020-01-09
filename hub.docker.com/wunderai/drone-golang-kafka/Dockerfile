FROM golang:1.12.5-alpine3.9
RUN apk update
RUN apk upgrade
RUN apk add --no-cache build-base alpine-sdk busybox-extras ca-certificates
RUN apk add --no-cache libgcc libressl-dev libsasl libstdc++ lz4-libs musl zlib-dev bzr
RUN apk add --no-cache bash mercurial
RUN git clone https://github.com/edenhill/librdkafka.git
RUN cd librdkafka && ./configure --prefix /usr && make && make install
RUN GO111MODULE=off go get -u github.com/ory/go-acc
RUN GO111MODULE=off wget -O - -q https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh -s -- -b $(go env GOPATH)/bin v1.16.0
#RUN apk add --no-cache graphviz ttf-freefont
#RUN GO111MODULE=off go get -u github.com/360EntSecGroup-Skylar/goreporter
RUN GO111MODULE=off go get -t golang.org/x/tools/cmd/goimports/...

RUN GO111MODULE=off go get github.com/ory/go-acc

# Install GOS for GOPROXY Support on private repos
RUN wget -O - -q https://github.com/storyicon/gos/releases/download/v1.1.0/linux_amd64.zip > /tmp/gos.zip \
    && unzip /tmp/gos.zip \
    && mv ./linux_amd64 /usr/local/bin/gos \
    && chmod 0755 /usr/local/bin/gos \
    && rm -rf /tmp/gos.zip

# Install goreportcard-cli
RUN curl -L https://git.io/vp6lP | sh && mv ./bin/* /usr/local/bin/. && rm -rf ./bin
RUN GO111MODULE=off go get github.com/gojp/goreportcard/cmd/goreportcard-cli
