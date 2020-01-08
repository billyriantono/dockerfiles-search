FROM ubuntu:14.04

RUN apt-get update \
    && apt-get -y dist-upgrade \
    && apt-get install -y supervisor --no-install-recommends \
    && apt-get clean \
    && apt-get autoclean \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*

RUN touch /etc/supervisor.conf \
    && echo "[supervisord]" > /etc/supervisor.conf \
    && echo "nodaemon=true" >> /etc/supervisor.conf \
    && echo "[include]" >> /etc/supervisor.conf \
    && echo "files = /etc/supervisor/conf.d/*.conf" >> /etc/supervisor.conf

CMD ["supervisord", "-c", "/etc/supervisor.conf"]

