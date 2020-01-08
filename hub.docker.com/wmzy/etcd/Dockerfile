FROM alpine:3.5

RUN         apk add --no-cache openssl && \
            wget https://github.com/coreos/etcd/releases/download/v2.3.5/etcd-v2.3.5-linux-amd64.tar.gz && \
            tar xzvf etcd-v2.3.5-linux-amd64.tar.gz && \
            mv etcd-v2.3.5-linux-amd64/etcd /bin/ && \
            apk del openssl && \
            rm -rf etcd-v2.3.5-linux-amd64*
VOLUME      /data
EXPOSE      4001 7001
ENTRYPOINT  ["/bin/etcd"]
CMD         ["-data-dir=/data"]
