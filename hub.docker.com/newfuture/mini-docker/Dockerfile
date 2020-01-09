FROM alpine:latest
MAINTAINER New Future <docker@newfuture.cc>

LABEL Name="mini-docker-mysql" Description="mimimal docker image for MySQL"

ENV DIR="/newfuture/mysql"
WORKDIR $DIR

COPY run.sh /run.sh

RUN apk add --no-cache \
    mysql \
 && addgroup mysql mysql \
 && rm -rf /var/lib/mysql \
        /var/cache/apk/* \
        /var/tmp/* \
        /tmp/* \
        /etc/ssl/* \
        /usr/include/*

VOLUME /var/lib/mysql /var/log/mysql /etc/mysql/ $DIR

EXPOSE 3306
USER mysql

ENTRYPOINT [ "/run.sh" ]
CMD [ "mysqld", "--user=mysql" ]
