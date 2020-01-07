FROM elasticsearch:1.7

RUN plugin -install mobz/elasticsearch-head

ENV ETCD_KEY /elasticsearch

ENV ETCDCTL_VERSION=v2.2.0

RUN curl -L  https://github.com/coreos/etcd/releases/download/$ETCDCTL_VERSION/etcd-$ETCDCTL_VERSION-linux-amd64.tar.gz -o /tmp/etcd-$ETCDCTL_VERSION-linux-amd64.tar.gz \
    && cd /tmp && tar xzvf etcd-$ETCDCTL_VERSION-linux-amd64.tar.gz \
    && cd etcd-$ETCDCTL_VERSION-linux-amd64 \
    && cp etcdctl /usr/local/bin \
    && chmod +x /usr/local/bin \
    && cd / && rm -rf /tmp/etcd-$ETCDCTL_VERSION/*

COPY entrypoint.sh /
RUN chmod +x entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
