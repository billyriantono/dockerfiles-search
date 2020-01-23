FROM debian:buster-slim
# hadolint ignore=DL3008
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        clamav-daemon \
        clamav-freshclam \
        netcat-openbsd \
        procps \
    && \
    freshclam --verbose --stdout && \
    install -d -m 755 -o clamav -g clamav /run/clamav && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /var/cache/apt/archives/*
COPY --chown=root:root clamd.conf /etc/clamav/
RUN clamconf -n
COPY --chown=root:root clamd-ping /usr/local/bin/
COPY --chown=root:root clamd-update /usr/local/bin/
USER clamav
WORKDIR /var/lib/clamav
EXPOSE 3310
CMD [ "clamd" ]
HEALTHCHECK CMD clamd-ping
