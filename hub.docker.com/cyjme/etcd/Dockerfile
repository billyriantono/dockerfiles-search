FROM alpine:latest
ARG ETCD_VERSION=3.3.12
VOLUME /var/lib/etcd/

RUN wget https://github.com/etcd-io/etcd/releases/download/v${ETCD_VERSION}/etcd-v${ETCD_VERSION}-linux-amd64.tar.gz && \
    tar -zxvf etcd-v${ETCD_VERSION}-linux-amd64.tar.gz && \
    mv etcd-v${ETCD_VERSION}-linux-amd64/etcd /usr/local/bin/ && \
    mv etcd-v${ETCD_VERSION}-linux-amd64/etcdctl /usr/local/bin/

EXPOSE 2379 2380
ENTRYPOINT ["etcd", "--data-dir", "/var/lib/etcd/"]
