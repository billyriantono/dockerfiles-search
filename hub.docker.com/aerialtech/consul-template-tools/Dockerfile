FROM debian:stretch-slim

# Consul options
ENV CONSUL_TEMPLATE_VERSION=0.19.5 CONSUL_SERVER=127.0.0.1:8500

# Consul-template install
RUN apt-get update && \
  apt-get -y install curl wget unzip && \
  mkdir -p /tmp/consul-template && \
  cd /tmp/consul-template && \
  wget https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip && \
  unzip consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip && \
  cp consul-template /usr/local/bin/consul-template && \
  rm -rf /tmp/consul-template && \
  rm -rf /var/lib/apt/lists/*
