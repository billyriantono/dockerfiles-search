FROM ubuntu:trusty

MAINTAINER statianzo

ENV DEBIAN_FRONTEND noninteractive
ENV ETCD_NODE 172.17.42.1:4001

RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup
RUN echo "exit 101" > /usr/sbin/policy-rc.d

RUN LC_ALL=C \
    apt-get update -y && \
    apt-get install -y   \
    haproxy \
    wget \
    supervisor

RUN sed -i 's/^ENABLED=.*/ENABLED=1/' /etc/default/haproxy

RUN rm -rf /var/cache/apt/* /var/lib/apt/lists/*

RUN wget -q https://github.com/kelseyhightower/confd/releases/download/v0.6.0-alpha3/confd-0.6.0-alpha3-linux-amd64 \
    -O /bin/confd && \
    chmod +x /bin/confd

CMD supervisord

ADD confd /etc/confd
ADD supervisor /etc/supervisor
ADD haproxy /etc/haproxy

