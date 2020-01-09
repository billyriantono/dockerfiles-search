FROM debian:jessie-backports

ARG dumb_init_v
ENV dumb_init_v ${dumb_init_v:-1.2.0}

RUN apt-get update && \
    apt-get install -y wget collectd && \
    rm -rf /var/lib/apt/lists/* && \
    wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_${dumb_init_v}_amd64.deb && \
    dpkg -i dumb-init_${dumb_init_v}_amd64.deb && rm dumb-init_${dumb_init_v}_amd64.deb && \
    apt-get purge -y wget && \
    mkdir -p /etc/collectd/collectd.conf.d

COPY collectd.conf /etc/collectd/collectd.conf
ENTRYPOINT ["/usr/bin/dumb-init", "--", "/usr/sbin/collectd", "-f", "-C", "/etc/collectd/collectd.conf"]
