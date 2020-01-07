FROM alpine:latest
MAINTAINER Alexander Baturin <alex.baturin1987@gmail.com>

ENV MYSQL_ROOT_PASSWORD=""
ENV MYSQL_DATABASE=""
ENV MYSQL_USER=""
ENV MYSQL_PASSWORD=""

WORKDIR /db
VOLUME /db
COPY startup.sh /startup.sh
RUN chmod +x /startup.sh

RUN apk add --update mysql mysql-client && rm -f /var/cache/apk/*
COPY my.cnf /etc/mysql/my.cnf

EXPOSE 3306
CMD ["/startup.sh"]