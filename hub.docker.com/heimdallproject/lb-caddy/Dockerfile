# A lightweight Caddy container that automatically proxies traffic to the backend Heimdall API servers.
FROM alpine:latest

LABEL caddy_version="0.10.2" architecture="amd64"

RUN apk add --no-cache openssh-client tar curl bash

RUN curl --silent --show-error --fail --location \
      --header "Accept: application/tar+gzip, application/x-gzip, application/octet-stream" -o - \
      "https://caddyserver.com/download/linux/amd64?plugins=${plugins}" \
    | tar --no-same-owner -C /usr/bin/ -xz caddy \
    && chmod 0755 /usr/bin/caddy \
    && /usr/bin/caddy -version

# Create empty directories for Consul config and data
RUN mkdir -p /etc/consul \
    && mkdir -p /var/lib/consul \
	&& mkdir /config \
	&& mkdir -p /var/consul

# Add Consul from https://releases.hashicorp.com/consul
RUN export CONSUL_VERSION=0.8.1 \
    && curl --retry 7 --fail -kvo /tmp/consul.zip "https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip" \
    && unzip /tmp/consul -d /usr/local/bin \
    && rm /tmp/consul.zip

# Install Consul template
# Releases at https://releases.hashicorp.com/consul-template/
RUN export CONSUL_TEMPLATE_VERSION=0.18.2 \
    && curl --retry 7 --fail -kLso /tmp/consul-template.zip "https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip" \
    && unzip /tmp/consul-template.zip -d /usr/local/bin \
    && rm /tmp/consul-template.zip

# Add Containerpilot and set its configuration
ENV CONTAINERPILOT_VER 2.7.3
ENV CONTAINERPILOT file:///etc/containerpilot.json

RUN curl -kLso /tmp/containerpilot.tar.gz \
         "https://github.com/joyent/containerpilot/releases/download/${CONTAINERPILOT_VER}/containerpilot-${CONTAINERPILOT_VER}.tar.gz" \
    && tar zxf /tmp/containerpilot.tar.gz -C /bin \
    && rm /tmp/containerpilot.tar.gz

# Add our configuration files and scripts
COPY etc /etc
COPY bin /usr/local/bin

# Consul session data written here
RUN mkdir -p /var/consul

EXPOSE 80 443

CMD [ "/bin/containerpilot", \
    "/usr/bin/caddy", \
        "--conf", \
        "/etc/caddyfile", \
        "--log", \
        "stdout"]