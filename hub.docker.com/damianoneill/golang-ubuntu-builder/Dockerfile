FROM golang:1.12.7-stretch

RUN apt-get update && \
    apt-get -y --no-install-recommends install git make && \
    rm -rf /var/lib/apt/lists/*

# https://github.com/docker-library/golang/issues/284
RUN set -ex; \
    echo 'deb http://deb.debian.org/debian buster main contrib non-free' > /etc/apt/sources.list.d/buster.list; \
    apt-get update && \
    apt-get -y --no-install-recommends install --upgrade openssl && \
    rm -rf /var/lib/apt/lists/* /etc/apt/sources.list.d/buster.*

# using latest as I dont want to manage versions for these, will 
# be updated when the base is moved forward
RUN go get -u github.com/golang/dep/cmd/dep
RUN go get -u github.com/golangci/golangci-lint/cmd/golangci-lint
RUN go get -u github.com/mcubik/goverreport
RUN go get -v -u github.com/go-lintpack/lintpack/...
RUN go get -u github.com/go-critic/go-critic/...
RUN lintpack build -o gocritic -linter.name='gocritic' github.com/go-critic/go-critic/checkers && mv gocritic /go/bin/
RUN go get -u github.com/elliotchance/ghost

ENV GO111MODULE=auto

CMD ["/bin/sh"]
