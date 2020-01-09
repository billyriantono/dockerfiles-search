FROM ubuntu:18.10

RUN apt-get update && apt-get install -y nano cron mysql-client tar gzip

ENV MYSQL_USER mysql_user
ENV MYSQL_PASSWORD mysql_password
ENV MYSQL_DATABASE mysql_database
ENV MYSQL_HOST mysql_host

COPY ./backup.sh /root/backup.sh
RUN chmod u+x /root/backup.sh
RUN mkdir -p /home/backup/web /home/backup/mysql

COPY ./root /var/spool/cron/crontabs/root
RUN chown root:crontab /var/spool/cron/crontabs/root
RUN chmod 600 /var/spool/cron/crontabs/root
RUN service cron start

COPY ./run.sh /run.sh
RUN chmod u+x /run.sh

ENTRYPOINT ["/run.sh"]
CMD cron && exec /bin/bash -c "trap : TERM INT; sleep infinity & wait"
