FROM alpine:latest AS builder

ARG ETCD_VERSION=3.3.10

ADD https://github.com/etcd-io/etcd/releases/download/v${ETCD_VERSION}/etcd-v${ETCD_VERSION}-linux-amd64.tar.gz /tmp/

RUN apk add --no-cache \
    bzip2 \
    make && \
    tar --strip-components=1 -zxf /tmp/etcd-v${ETCD_VERSION}-linux-amd64.tar.gz -C /tmp

FROM alpine:latest

COPY --from=builder /tmp/etcd /usr/local/bin/etcd

COPY --from=builder /tmp/etcdctl /usr/local/bin/etcdctl

CMD [ "etcd" ]