FROM debian:buster-slim
# hadolint ignore=DL3008
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        gnupg \
        libmail-spf-perl \
        sa-compile \
        spamassassin \
        spamc \
    && \
    usermod --append --groups mail debian-spamd && \
    install -m 640 -o debian-spamd -g debian-spamd /dev/null /var/run/spamd.pid && \
    install -d -m 750 -o debian-spamd -g debian-spamd /run/spamd && \
    install -d -m 750 -o debian-spamd -g debian-spamd /var/backups/sa-learn && \
    rm -rf /run/spamd/* /var/backups/sa-learn/* && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /var/cache/apt/archives/*
COPY --chown=root:root entrypoint spamd-ping spamd-learn spamd-update /usr/local/bin/
USER debian-spamd
WORKDIR /var/lib/spamassassin
RUN spamd-update
EXPOSE 7783
VOLUME /run/spamd
VOLUME /var/backups/sa-learn
ENTRYPOINT [ "entrypoint" ]
CMD [ "spamd", "--create-prefs", "--max-children=5", "--helper-home-dir", "--listen=0.0.0.0:7783", "--socketpath=/var/run/spamd/spamd.sock", "--syslog=stderr", "--pidfile=/var/run/spamd.pid" ]
HEALTHCHECK CMD spamd-ping
