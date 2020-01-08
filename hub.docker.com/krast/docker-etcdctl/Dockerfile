FROM alpine:latest
RUN apk update && apk add tar
WORKDIR /opt
ENV ETCD_VERSION=3.2.13
ADD https://github.com/coreos/etcd/releases/download/v$ETCD_VERSION/etcd-v$ETCD_VERSION-linux-amd64.tar.gz .
RUN tar -xvf etcd-v$ETCD_VERSION-linux-amd64.tar.gz

FROM alpine:latest
RUN apk update && apk add ca-certificates
WORKDIR /usr/local/bin/
ENV ETCD_VERSION=3.2.13
COPY --from=0 /opt/etcd-v$ETCD_VERSION-linux-amd64/etcdctl .
ENTRYPOINT ["/usr/local/bin/etcdctl"]
