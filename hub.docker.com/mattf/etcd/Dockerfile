FROM fedora:latest

MAINTAINER Matthew Farrellee <matt@cs.wisc.edu>

RUN yum update -y && \
    yum install -y https://kojipkgs.fedoraproject.org//packages/etcd/2.0.5/0.1.fc23/x86_64/etcd-2.0.5-0.1.fc23.x86_64.rpm

WORKDIR /var/lib/etcd/

EXPOSE 4001

ENTRYPOINT ["etcd", "--listen-client-urls", "http://0.0.0.0:4001"]
