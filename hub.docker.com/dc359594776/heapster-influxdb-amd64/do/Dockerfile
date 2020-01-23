# Consul server

FROM datamgtcloud/baseconsul
MAINTAINER Changbing JI

RUN \
  mkdir -p /opt/datamgt/home/util/consul_ui && \
  curl -s https://releases.hashicorp.com/consul/0.6.4/consul_0.6.4_web_ui.zip -o /opt/datamgt/home/util/consul_ui/ui.zip && \
  cd /opt/datamgt/home/util/consul_ui && \
  unzip ui.zip && \
  rm ui.zip

COPY docker/consul.d/ /etc/consul.d/

# Make server data persistent
VOLUME /data
RUN \
  mkdir /data/consul && \
  ln -s /data/consul /opt/datamgt/config/srv/consul

EXPOSE 53/udp 53 8300 8302 8302/udp 8400 8500

CMD ["/sbin/boot"]
