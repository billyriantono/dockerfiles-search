FROM alpine:latest

MAINTAINER IPBurger <accounts@ipburger.com>
MAINTAINER Daisuke Baba

RUN apk add --no-cache \
    mysql-client python-dev py-pip bash openrc \
    linux-headers musl-dev gcc

RUN pip install python-swiftclient python-keystoneclient

ENV DBS="" MYSQL_HOST="mysql" STORAGE_TYPE="local" PREFIX="" MAX_BACKUP_FILES="7"
ENV BACKUP_DIR=""

COPY backup.sh restore.sh _list.sh delete.sh /
COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]
CMD ["/usr/sbin/crond", "-f"]
