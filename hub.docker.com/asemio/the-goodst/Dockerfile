FROM postgres:9.4.10

RUN localedef -i de_DE -c -f UTF-8 -A /usr/share/locale/locale.alias de_DE.UTF-8
ENV LANG de_DE.utf8

ADD init-user-db.sh /docker-entrypoint-initdb.d/init-user-db.sh
RUN chmod 755 /docker-entrypoint-initdb.d/init-user-db.sh
