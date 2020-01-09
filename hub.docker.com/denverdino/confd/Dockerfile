FROM debian:wheezy
ENV VERSION 0.8.0
ENV ETCD_HOST '127.0.0.1:2379'
ENV INTERVAL 10
ADD https://drone.io/github.com/denverdino/confd-helper/files/confd-helper /usr/local/bin/confd-helper
ADD https://github.com/kelseyhightower/confd/releases/download/v${VERSION}/confd-${VERSION}-linux-amd64 /usr/local/bin/confd
RUN chmod +x /usr/local/bin/confd && chmod +x /usr/local/bin/confd-helper && mkdir -p /etc/confd/templates
CMD confd -verbose -watch -interval $INTERVAL -node $ETCD_HOST
