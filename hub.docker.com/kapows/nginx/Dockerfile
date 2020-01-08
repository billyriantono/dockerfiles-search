FROM nginx:1.15.2

ADD https://dl.eff.org/certbot-auto /usr/bin/certbot-auto
RUN chmod a+x /usr/bin/certbot-auto && \
  certbot-auto -n --os-packages-only && \
  apt update && \
  apt install -y cron && \
  echo "16 4,16 * * * certbot-auto renew" > /tmp/cert-renew && \
  crontab /tmp/cert-renew && \
  rm /tmp/cert-renew