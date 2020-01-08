FROM leifg/postgres-s3-backup
LABEL maintainer="Leif Gensert <leif@leif.io>"

ENTRYPOINT ["crond", "-f"]

RUN mkdir /scripts
ADD scripts/* /scripts/

RUN echo '0 2 * * * /scripts/backup_release_ping_eventstore.sh > /proc/1/fd/1 2>&1' >> /var/spool/cron/crontabs/root
RUN echo '0 2 * * * /scripts/backup_release_ping_readstore.sh > /proc/1/fd/1 2>&1' >> /var/spool/cron/crontabs/root
RUN echo '0 6 * * * /scripts/backup_hn_vanity_eventstore.sh > /proc/1/fd/1 2>&1' >> /var/spool/cron/crontabs/root
RUN echo '0 6 * * * /scripts/backup_hn_vanity_readstore.sh > /proc/1/fd/1 2>&1' >> /var/spool/cron/crontabs/root
RUN echo "" >> /var/spool/cron/crontabs/root
RUN crontab /var/spool/cron/crontabs/root
