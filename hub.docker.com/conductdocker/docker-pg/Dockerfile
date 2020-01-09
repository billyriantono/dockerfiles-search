FROM postgres

MAINTAINER Kim Daniel Engebretsen

ADD openidm.psql /docker-entrypoint-initdb.d/openidm.sql
RUN localedef -i nb_NO -c -f UTF-8 -A /usr/share/locale/locale.alias nb_NO.UTF-8
ENV LANG nb_NO.utf8
ENV POSTGRES_USER openidm
ENV POSTGRES_PASSWORD openidm
