from webwurst/ubuntu

run mkdir /tmp/etcd
run curl -L https://github.com/coreos/etcd/releases/download/v0.4.3/etcd-v0.4.3-linux-amd64.tar.gz |\
  tar -xz --directory /tmp/etcd --strip-components 1
run cp /tmp/etcd/etcd /usr/local/bin/
run cp /tmp/etcd/etcdctl /usr/local/bin/

add etcd_start /usr/local/bin/
run chmod +x /usr/local/bin/etcd_start

expose 4001 7001
cmd ["/usr/local/bin/etcd_start"]