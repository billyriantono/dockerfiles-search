FROM tor2/centos-source-base:4.0.0
MAINTAINER Kolla Project (https://launchpad.net/kolla)








RUN usermod --append --home /var/lib/haproxy --groups kolla haproxy \
    && mkdir -p /var/lib/haproxy \
    && chown -R 42454:42454 /var/lib/haproxy





RUN yum -y install haproxy socat && yum clean all

RUN mkdir -p /var/lib/kolla/haproxy \
    && chown -R haproxy: /var/lib /run

COPY ensure_latest_config.sh /usr/local/bin/kolla_ensure_haproxy_latest_config
RUN chmod 755 /usr/local/bin/kolla_ensure_haproxy_latest_config


