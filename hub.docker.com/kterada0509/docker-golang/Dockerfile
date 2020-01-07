FROM centos:7

ENV GOLANG_VERSION 1.9

ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA256 d70eadefce8e160638a9a6db97f7192d8463069ab33138893ad3bf31b0650a79

RUN yum update -y                                    \
    && yum install -y wget                           \
    git                                              \
    tar                                              \
    g++                                              \
    gcc                                              \
    libc6-dev                                        \
    make                                             \
    python-setuptools

RUN set -eux; \
    \
    curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz                \
    && echo "$GOLANG_DOWNLOAD_SHA256  golang.tar.gz" | sha256sum -c - \
    && tar -C /usr/local -xzf golang.tar.gz                           \
    && rm golang.tar.gz

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH