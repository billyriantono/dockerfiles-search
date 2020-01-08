FROM extvos/alpine
MAINTAINER  "Mingcai SHEN <archsh@gmail.com>"
ENV ETCD_VER v3.2.4
ENV DOWNLOAD_URL https://github.com/coreos/etcd/releases/download

RUN curl -L ${DOWNLOAD_URL}/${ETCD_VER}/etcd-${ETCD_VER}-linux-amd64.tar.gz -o /tmp/etcd-${ETCD_VER}-linux-amd64.tar.gz \
	&& mkdir /usr/local/etcd-${ETCD_VER} \
	&& tar xzvf /tmp/etcd-${ETCD_VER}-linux-amd64.tar.gz -C /usr/local/etcd-${ETCD_VER} --strip-components=1 \
	&& ln -s /usr/local/etcd-${ETCD_VER}/etcd /usr/bin/etcd \
	&& ln -s /usr/local/etcd-${ETCD_VER}/etcdctl /usr/bin/etcdctl

EXPOSE 2379
EXPOSE 2380

CMD ["/usr/bin/etcd"]
