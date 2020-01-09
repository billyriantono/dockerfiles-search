FROM rancher/server:latest

COPY opt /opt

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    supervisor && \
    rm -rf /var/lib/apt/lists/* && \
    chmod +x /opt/caddy/caddy && \
    rm -rf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord","-c","/opt/supervisord/my.conf"]