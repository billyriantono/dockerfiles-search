FROM chentung/base:latest
LABEL maintainer="chentung <chentung.wu@outlook.com>"

RUN apk add --update mysql mysql-client \
    && rm -rf /var/cache/apk/*

COPY entrypoint.sh /entrypoint.sh
COPY my.cnf /etc/mysql/my.cnf

RUN chmod a+x /entrypoint.sh

EXPOSE 3306

ENTRYPOINT ["/entrypoint.sh"]
