FROM codeblick/php:7.1-apache

ENV DEBIAN_FRONTEND noninteractive

ADD init-db.sh /usr/local/bin/init-db.sh

RUN apt-get update -qq && \
    apt-get install -y -qq mysql-server && \
    chmod +x /usr/local/bin/init-db.sh

ADD my.cnf /etc/mysql/conf.d/my.cnf

EXPOSE 3306

CMD /usr/local/bin/init-db.sh; /usr/sbin/mysqld & apache2-foreground
