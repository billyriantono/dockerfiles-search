FROM kz8s/centos
MAINTAINER Jono Wells <jono@kz8s.io>

ENV BASEURL https://github.com/coreos/etcd/releases/download
ENV VERSION v2.3.0

RUN set -ex &&\
  curl -L $BASEURL/$VERSION/etcd-$VERSION-linux-amd64.tar.gz | tar xzvf -

WORKDIR /etcd-$VERSION-linux-amd64

EXPOSE 4001 7001 2379 2380
ENTRYPOINT [ "./etcd" ]
