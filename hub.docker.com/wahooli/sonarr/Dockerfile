ARG SONARR_VERSION="latest"
FROM linuxserver/sonarr:${SONARR_VERSION}

ENV HTTP_PORT="80" \
    HTTPS_PORT="443" \
    ENABLE_SSL="False" \
    LOG_LEVEL="Info" \
    BIND_ADDRESS="*"

EXPOSE 80/tcp
EXPOSE 443/tcp

COPY config /config

RUN apt-get update \
    && apt-get install -y libcap2-bin \
    && rm -rf \
       /tmp/* \
       /var/lib/apt/lists/* \
       /var/tmp/* \
    && setcap 'cap_net_bind_service=+ep' $(realpath $(which mono)) \
    && chown abc:abc /config/config.xml
