FROM alpine:latest 
MAINTAINER "Levent SAGIROGLU" <LSagiroglu@gmail.com>
ARG VERSION=v3.3.0
RUN apk add --update --no-cache openssl tar tzdata ca-certificates && \
       update-ca-certificates && \
       cp /usr/share/zoneinfo/Europe/Istanbul /etc/localtime && \
       echo "Europe/Istanbul" >  /etc/timezone && \
       wget https://github.com/coreos/etcd/releases/download/${VERSION}/etcd-${VERSION}-linux-amd64.tar.gz && \
       tar xzvf etcd-${VERSION}-linux-amd64.tar.gz && \
       mv etcd-${VERSION}-linux-amd64/etcd* /bin/ && \
    apk del --purge tzdata tar openssl && \
    rm -Rf etcd-${VERSION}-linux-amd64* /var/cache/apk/*
VOLUME /srv 
COPY bin /bin
COPY etc/etcd /etc/etcd
WORKDIR /bin
ENV ETCDCONF "/etc/etcd/etcd.conf.yml" 
EXPOSE 2379 2380 4001 7001 

ENTRYPOINT ["/bin/entrypoint.sh"]

# docker run -d -p 2379:2379  -p 2380:2380  -p 4001:4001  -p 7001:7001  -v D:\Docker\hasweb:/data   --name some-etcd   etcd  -name etcd1
