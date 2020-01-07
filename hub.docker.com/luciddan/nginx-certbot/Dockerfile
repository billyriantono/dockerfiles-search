FROM certbot/certbot:latest

WORKDIR /app

COPY ./app .
# Run our python script every hour to update our nginx and certbot config
COPY certbot-hourly.crontab /etc/periodic/hourly/certbot-renew
COPY certbot-daily.crontab /etc/periodic/daily/certbot-vhosts

RUN apk add --no-cache --update bash python3 ca-certificates bash wget openssl \
    && update-ca-certificates \
    && mkdir -p /etc/nginx/conf.d /var/www/certbot \
	&& pip3 install --upgrade pip \
	&& pip3 install docker

ENV DOCKER_HOST unix:///tmp/docker.sock

VOLUME ["/etc/nginx/conf.d", "/etc/letsencrypt", "/var/www/certbot", "/tmp/docker.sock"]

ENTRYPOINT ["/usr/bin/env"]

CMD ["/bin/sh", "/app/launch.sh"]
