FROM owncloud
LABEL Name=docker-owncloud-ssl Version=0.0.1 

# Install certbot
RUN apt-get update && apt-get install -y --no-install-recommends wget && rm -rf /var/lib/apt/lists/*
WORKDIR /app
RUN wget https://dl.eff.org/certbot-auto 
RUN cp certbot-auto /usr/local/bin/
RUN chmod a+x /usr/local/bin/certbot-auto
RUN certbot-auto -n --os-packages-only && rm -rf /var/lib/apt/lists/*

# Run certbot on first start and set to update daily.
COPY owncloud-ssl-start.sh /usr/local/bin/
COPY certbot-update.sh /etc/cron.daily/
RUN chmod a+x /usr/local/bin/owncloud-ssl-start.sh && chmod a+x /etc/cron.daily/certbot-update.sh

# Switch back to the website directory so the owncloud script runs correctly.
WORKDIR /var/www/html

ENTRYPOINT [ "owncloud-ssl-start.sh" ]

CMD ["tail", "-f", "/var/log/apache2/access.log"]