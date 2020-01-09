# Dockerfile vps services


FROM debian:stretch-slim
LABEL maintainer="nobody"

ENV DEBIAN_FRONTEND noninteractive

# fix apt-utils warning
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

# install apps
RUN apt-get update \
	&& apt-get install -y openssl wget supervisor

RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisord.conf

# install shadowsocks-libev
RUN set -ex \
	&& printf "deb http://deb.debian.org/debian testing main" > /etc/apt/sources.list.d/testing.list \
	&& apt-get update \
	&& apt-get -t testing install -y --no-install-recommends shadowsocks-libev \
	&& rm -rf /var/lib/apt/lists/*
# v2ray-plugin
ENV V2RAY_PLUGIN_VERSION v1.2.0
RUN wget -O v2ray-plugin.tar.gz https://github.com/shadowsocks/v2ray-plugin/releases/download/${V2RAY_PLUGIN_VERSION}/v2ray-plugin-linux-amd64-${V2RAY_PLUGIN_VERSION}.tar.gz \
    && tar -xzf v2ray-plugin.tar.gz \
    && mv ./v2ray-plugin_linux_amd64 /usr/bin/v2ray-plugin \
    && rm -rf v2ray-plugin*

COPY shadowsocks-libev/*.json /etc/shadowsocks-libev/
COPY shadowsocks-libev/shadowsocks.sh /tmp/
RUN bash /tmp/shadowsocks.sh

# install frp
ENV FRP_VERSION 0.23.3

RUN set -ex \
	&& rm -rf /var/lib/apt/lists/* \
	&& cd /tmp \
	&& wget -O frp.tar.gz "https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz" \
	&& tar -xzf frp.tar.gz \
	&& mkdir -p /usr/local/frp/ \
	&& mv ./frp_${FRP_VERSION}_linux_amd64/frps /usr/local/frp/ \
        && rm frp.tar.gz \
	&& rm -rf /tmp/*
COPY frp/frps.ini /usr/local/frp/


ENTRYPOINT ["/usr/bin/supervisord"]

