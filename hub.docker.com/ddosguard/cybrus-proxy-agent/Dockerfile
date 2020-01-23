FROM debian:jessie

COPY ./cybrusserver-proxy-adapter_1.4.2.29272_amd64.deb /tmp

RUN set -x \
    && apt-get update \
    && apt-get install openssl -y \
    && apt-get autoremove \
    && apt-get autoclean \
    && dpkg -i /tmp/cybrusserver-proxy-adapter_1.4.2.29272_amd64.deb \
    && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apt/archives/*

CMD ["cybrus-proxy-adapter", "--config", "/etc/cybrus-proxy/proxy-adapter.config"]
