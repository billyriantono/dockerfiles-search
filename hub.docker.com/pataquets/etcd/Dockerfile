FROM coreos/etcd

ADD ./etcd-start /opt/etcd/bin/etcd-start

EXPOSE 4001 7001

ENTRYPOINT [ "/opt/etcd/bin/etcd-start" ]
