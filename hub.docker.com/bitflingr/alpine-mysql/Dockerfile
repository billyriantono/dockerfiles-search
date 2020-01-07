FROM alpine:latest
MAINTAINER Jarrett Irons <jarrett.irons@gmail.com>

WORKDIR /app
VOLUME /app
COPY startup.sh /startup.sh

RUN  apk add --no-cache mysql && rm -f /var/cache/apk/*
COPY my.cnf /etc/mysql/my.cnf

EXPOSE 3306
CMD ["/startup.sh"]
