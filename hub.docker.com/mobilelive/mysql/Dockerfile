FROM mobilelive/alpine:basic
MAINTAINER mobilelive/dockerfiles

# install #

RUN apk add --update \
      "mysql>10.1" \
      "mysql-client>10.1" \
      ;
RUN rm -rf /var/cache/apk/*

# setup #

RUN rm -rf /app/etc ; \
      mv -f /etc/mysql /app/etc ; \
      ln -s /app/etc /etc/mysql
RUN rm -rf /app/var ; \
      mv -f /var/lib/mysql /app/var ; \
      ln -s /app/var /var/lib/mysql

RUN mysql_install_db --user=mysql --ldata=/var/lib/mysql/
RUN chown -R app:app /app
RUN chown -R mysql:mysql /app/var

# cmd #

EXPOSE 3306
CMD [ "mysqld_safe" ]




