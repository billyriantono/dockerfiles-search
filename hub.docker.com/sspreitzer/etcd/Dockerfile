FROM centos:7

RUN yum install -y etcd && \
  yum clean all

VOLUME /var/lib/etcd
EXPOSE 2379 2380 4001 7001

USER etcd
WORKDIR /var/lib/etcd
CMD etcd --listen-peer-urls 'http://0.0.0.0:2380,http://0.0.0.0:7001' --listen-client-urls 'http://0.0.0.0:2379,http://0.0.0.0:4001' --advertise-client-urls 'http://etcd:2379,http://etcd:4001'
