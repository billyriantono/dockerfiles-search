FROM bmoorman/ubuntu:bionic

ENV TRANSMISSION_PORT="9091" \
    TRANSMISSION_ALLOWED="192.168.*.*,172.17.*.*"

ARG DEBIAN_FRONTEND="noninteractive"

RUN echo 'deb http://ppa.launchpad.net/transmissionbt/ppa/ubuntu bionic main' > /etc/apt/sources.list.d/transmission.list \
 && echo 'deb-src http://ppa.launchpad.net/transmissionbt/ppa/ubuntu bionic main' >> /etc/apt/sources.list.d/transmission.list \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 976B5901365C5CA1 \
 && apt-get update \
 && apt-get install --yes --no-install-recommends \
    curl \
    openssh-client \
    transmission-cli \
    transmission-daemon \
    unrar \
 && apt-get autoremove --yes --purge \
 && apt-get clean \
 && rm --recursive --force /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY transmission/ /etc/transmission/

VOLUME /config /data

EXPOSE ${TRANSMISSION_PORT}

CMD ["/etc/transmission/start.sh"]

HEALTHCHECK --interval=60s --timeout=5s CMD curl --head --insecure --silent --show-error --fail "http://localhost:${TRANSMISSION_PORT}/" || exit 1
