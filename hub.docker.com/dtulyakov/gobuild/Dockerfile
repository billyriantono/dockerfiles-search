FROM golang:1.12-alpine

ARG BUILD_DATE
ARG VCS_REF=master
ARG VERSION

LABEL maintainer="dtulyakov@gmil.com" \
  org.label-schema.build-date=$BUILD_DATE \
  org.label-schema.docker.cmd="docker run -v \${PWD}:/src dtulyakov/gobuild sh -c CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o hello hello.go" \
  org.label-schema.description="For build src code" \
  org.label-schema.name="gobuild" \
  org.label-schema.schema-version="1.12" \
  org.label-schema.url="https://golang.io/" \
  org.label-schema.vcs-ref=$VCS_REF \
  org.label-schema.vcs-url="https://bitbucket.org/dtulyakov/docker-gobuild" \
  org.label-schema.vendor="dtulyakov" \
  org.label-schema.version=$VERSION

RUN set -x \
  && apk add -q --update --clean-protected --no-cache \
    git \
    && rm -rf /var/cache/apk/*\
    && mkdir /.cache\
    && chmod 777 /.cache\
    && go get github.com/libp2p/go-reuseport \
    && go get github.com/ugorji/go/codec \
    && go get github.com/vmihailenco/msgpack \
    && go get github.com/nats-io/go-nats-streaming \
    && go get github.com/nats-io/go-nats \
    && go get gopkg.in/yaml.v2 \
    && go get github.com/fsnotify/fsnotify \
    && go get github.com/nats-io/go-nats \
    && go get github.com/vmihailenco/msgpack \
    && go get github.com/kshvakov/clickhouse \
    && go get github.com/oschwald/maxminddb-golang \
    && go get github.com/lib/pq \
    && go get github.com/patrickmn/go-cache \
    && go get github.com/spf13/viper \
    && go get go.etcd.io/etcd/clientv3

# vim: set filetype=dockerfile et sw=2 ts=2:
