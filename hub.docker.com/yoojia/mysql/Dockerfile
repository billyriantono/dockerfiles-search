FROM alpine:3.7

LABEL MAINTAINER="yoojiachen@gmail.com"

ENV LC_ALL=en_US.UTF-8

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.cloud.tencent.com/g' /etc/apk/repositories \
    && apk add tzdata mariadb mariadb-client \
    && rm -rf /var/cache/apk/*

RUN mkdir -p /run/mysqld/

COPY test /var/lib/mysql/scripts/
ONBUILD COPY scripts /var/lib/mysql/scripts/

VOLUME /var/lib/mysql
EXPOSE 3306

# Will change
COPY entrypoint.sh /entrypoint.sh
COPY my.cnf /etc/mysql/my.cnf

HEALTHCHECK CMD ["mysqladmin", "ping"]

ENTRYPOINT ["/entrypoint.sh"]
