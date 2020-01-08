FROM alpine:latest as downloader
RUN apk add curl bash
RUN curl -L https://github.com/etcd-io/etcd/releases/download/v3.3.18/etcd-v3.3.18-linux-amd64.tar.gz \
    -o etcd.tar.gz && tar -zxvf etcd.tar.gz etcd-v3.3.18-linux-amd64/etcdctl
RUN mv etcd-v3.3.18-linux-amd64/etcdctl /bin/etcdctl && \
    rm -Rf /workspace
ENV ETCDCTL_API 3
ENTRYPOINT [ "/bin/bash" ]
