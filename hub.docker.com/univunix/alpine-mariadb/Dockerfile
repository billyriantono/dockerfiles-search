FROM alpine:edge
MAINTAINER aglezabad@gmail.com

ENV LANG="en_GB.UTF-8" \
    LC_ALL="en_GB.UTF-8" \
    LANGUAGE="en_GB.UTF-8" \
		DB_ROOT_PASS="toor" \
    DB_USER="admin" \
    DB_PASS="password" \
    TERM="xterm"

RUN apk -U upgrade && \
    apk --update add \
      mariadb mariadb-client \
      && \
      rm -rf /tmp/src && \
      rm -rf /var/cache/apk/*


ADD ./files/my.cnf /etc/mysql/my.cnf
ADD ./files/start.sh /start.sh

RUN chmod u+x /start.sh

VOLUME ["/data"]
EXPOSE 3306

CMD ["/start.sh"]
