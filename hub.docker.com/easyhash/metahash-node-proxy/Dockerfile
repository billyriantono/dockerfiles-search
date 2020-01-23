FROM ubuntu:xenial
RUN apt update \
    && apt install -y nano curl libssl1.0.0

RUN curl -L -o metahash-proxy.deb https://github.com/metahashorg/node_proxy/releases/download/Proxy_v1.4/metahash-proxy_1.4.deb \
    && dpkg -i metahash-proxy.deb \
    && rm -f metahash-proxy.deb


WORKDIR /opt/proxy

ENV PROXY_KEY=key/proxy_key
ENV PROXY_CONFIG=proxy_config
ENV PROXY_PORT=9999
ENV PROXY_LIMIT=5000000

# Remember to map your HEX-private key to ${PROXY_KEY} via VOLUME or SECRET
# Run the following on the Docker host and reboot.
# echo '* - core unlimited' >>/etc/security/limits.conf
CMD ./proxy ${PROXY_KEY} ${PROXY_CONFIG} ${PROXY_PORT} ${PROXY_LIMIT}
