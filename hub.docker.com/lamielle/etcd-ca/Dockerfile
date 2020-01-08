FROM progrium/busybox
MAINTAINER Alan LaMielle <alan.lamielle+github@gmail.com>

ADD https://github.com/lamielle/etcd-ca/releases/download/v0.1.0/etcd-ca_0.1.0_linux_amd64.tar.gz /tmp/etcd-ca.tgz
RUN cd /bin && gzip -dc /tmp/etcd-ca.tgz | tar -xf - && rm /tmp/etcd-ca.tgz

ENTRYPOINT ["/bin/etcd-ca"]
