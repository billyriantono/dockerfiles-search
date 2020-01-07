FROM ubuntu:18.04

MAINTAINER Guido Kovacs <kovacs.guido@gmail.com>

RUN apt-get update \
    && apt-get -y install -qq --force-yes mysql-client cron bzip2 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir /backups

ENV MYSQL_ENV_MYSQL_HOST mysql
ENV BACKUP_TIME 0 2 * * *

COPY docker-entrypoint.sh /entrypoint.sh
COPY backup restore /bin/
RUN chmod +x /entrypoint.sh \
    && chmod +x /bin/backup \
    && chmod +x /bin/restore

VOLUME /backups

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/usr/sbin/cron", "-f"]