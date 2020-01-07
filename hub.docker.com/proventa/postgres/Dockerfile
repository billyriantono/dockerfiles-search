FROM postgres:11

RUN localedef -i de_DE -c -f UTF-8 -A /usr/share/locale/locale.alias de_DE.UTF-8
ENV LANG de_DE.utf8

COPY ./initdb.d/* /docker-entrypoint-initdb.d/

COPY docker-postgres-entrypoint /usr/local/bin/
ENTRYPOINT ["docker-postgres-entrypoint"]
CMD ["postgres"]
