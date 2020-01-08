FROM alpine:3.9
MAINTAINER paladintyrion <paladintyrion@gmail>

ENV MYSQL_LOG /app/mysql/log

RUN set -x \
    && apk update \
    && apk add --no-cache bash tzdata \
    && rm -f /etc/localtime \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && mkdir -p /run/mysqld ${MYSQL_LOG} \
    && apk add --no-cache mysql mysql-client \
    && rm -rf /var/cache/apk/* \
    && set +x

COPY my.cnf /etc/my.cnf
COPY start_mysqld.sh /app/mysql/start_mysqld.sh
RUN chmod +x /app/mysql/start_mysqld.sh

WORKDIR /app/mysql
VOLUME ["/var/lib/mysql", "/app/mysql/log"]
EXPOSE 3306

ENTRYPOINT ["/app/mysql/start_mysqld.sh"]
CMD ["mysqld", "--user=root"]
