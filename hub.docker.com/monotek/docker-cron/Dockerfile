FROM debian

RUN apt-get update \
    && apt-get -y install cron mysql-client

COPY cronjobs /etc/cron.d/cronjobs

COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["cron"]
