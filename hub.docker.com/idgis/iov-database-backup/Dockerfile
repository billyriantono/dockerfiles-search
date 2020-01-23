FROM ubuntu:18.04

# Install software
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        cron \
        duplicity \
        lftp \
        postgresql-client-10 \
        python-paramiko \
        openssh-client \
    && rm -rf /var/lib/apt/lists/*

COPY backup.sh /opt/
COPY start.sh /opt/

RUN chmod u+x /opt/*.sh

VOLUME /backup

HEALTHCHECK --interval=5s --timeout=3s --retries=3 CMD exit 0

CMD ["/opt/start.sh"]
