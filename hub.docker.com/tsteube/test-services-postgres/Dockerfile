FROM postgres:11.1-alpine
MAINTAINER Thorsten Steube <tsteube@gmx.de>
 
RUN apk update && apk add findutils && rm -rf /var/cache/apk/*

#RUN localedef -i de_DE -c -f UTF-8 -A /usr/share/locale/locale.alias de_DE.UTF-8
#ENV LANG de_DE.utf8

# setup database folder structure for backup and archive
RUN mkdir /var/lib/postgresql/archive /var/lib/postgresql/backup && \
  chown postgres:postgres /var/lib/postgresql/archive /var/lib/postgresql/backup
COPY pg_maintenance.sh /var/lib/postgresql/pg_maintenance.sh
COPY postgres-initdb.d /docker-entrypoint-initdb.d

WORKDIR /var/lib/postgresql/