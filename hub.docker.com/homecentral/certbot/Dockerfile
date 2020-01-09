FROM certbot/dns-cloudflare

ENV DOMAIN=undefined
ENV EMAIL=undefined

ADD run-certbot.sh /run-certbot.sh
ADD certbot-cron /etc/crontabs/root
ADD entrypoint.sh /entrypoint.sh

RUN chmod +x /etc/crontabs/root && \
    chmod +x /entrypoint.sh && \
    chmod +x /run-certbot.sh && \
    mkdir -p /etc/letsencrypt

VOLUME /cloudflare-credentials.ini
VOLUME /etc/letsencrypt/output

ENTRYPOINT [ "/bin/sh", "/entrypoint.sh" ]