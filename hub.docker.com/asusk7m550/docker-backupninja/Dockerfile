FROM ubuntu:18.04

RUN apt update && apt install -y backupninja ssh rdiff rdiff-backup mysql-client && apt clean

ADD files/entrypoint.sh /usr/local/bin/entrypoint.sh

VOLUME /etc/backup.d

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

CMD ["/usr/sbin/backupninja", "-d", "-n"]
