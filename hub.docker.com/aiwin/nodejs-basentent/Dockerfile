FROM golang:1.12.4 as builder

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh -s v1.16.0 -b "$(go env GOPATH)/bin" && \
  go get -u mvdan.cc/sh/cmd/shfmt \
    mvdan.cc/gofumpt \
    mvdan.cc/unindent \
    github.com/agflow/splint \
    github.com/pavius/impi/cmd/impi \
    github.com/m3db/build-tools/linters/badtime \
    github.com/hypnoglow/durcheck \
    github.com/nishanths/predeclared \
    github.com/elliotchance/ghost \
    github.com/Quasilyte/go-consistent

FROM golang:1.12.4
COPY --from=builder /go/bin/* /usr/bin/

WORKDIR /go
