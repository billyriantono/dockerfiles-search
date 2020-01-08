FROM dock0/service
MAINTAINER Jon Chen <bsd@voltaire.sh>

VOLUME /opt/etcd-ca/

ADD https://dl.bintray.com/jchen/docku/latest/etcd-ca /usr/sbin/etcd-ca
RUN chmod +x /usr/sbin/etcd-ca

RUN mkdir -p /opt/etcd-ca/

WORKDIR /opt/etcd-ca
ENTRYPOINT ["/usr/sbin/etcd-ca"]
