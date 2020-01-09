FROM debian:stable-slim

MAINTAINER Alex Wang <ialexwwang@gmail.com>

RUN apt-get update \
    && apt-get install -y --no-install-recommends stunnel4 \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /etc/stunnel \
    && sed -i 's/ENABLE=0/ENABLE=1/' /etc/default/stunnel4 \
    && sed -i 's/RLIMITS=""/RLIMITS="-n 4096"/' /etc/default/stunnel4 \
    && ln -s /config /etc/stunnel

VOLUME ["/config", "/certs"]
WORKDIR /config
# runtime configuration
EXPOSE 443

ENTRYPOINT ["stunnel4"]

