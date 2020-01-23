FROM quay.io/coreos/etcd:v3.0.8

EXPOSE 4001
EXPOSE 2379

ENTRYPOINT ["/usr/local/bin/etcd"]

CMD ["--listen-client-urls", \
    "http://0.0.0.0:2379,http://0.0.0.0:4001", \
    "--advertise-client-urls", \
    "http://0.0.0.0:2379,http://0.0.0.0:4001"]