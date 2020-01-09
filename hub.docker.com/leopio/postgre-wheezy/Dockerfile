FROM debian:wheezy

RUN apt-get update -qq && apt-get upgrade -y
RUN apt-get install wget -qq

RUN apt-get install -y ca-certificates
RUN wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb
RUN dpkg -i dumb-init_*.deb

RUN groupadd -r postgres --gid=999 && useradd -r -g postgres --uid=999 postgres

RUN touch /etc/apt/sources.list.d/pgdg.list
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ wheezy-pgdg main" > /etc/apt/sources.list.d/pgdg.list

RUN apt-key update && apt-get update && apt-get install --force-yes -y postgresql-9.4 postgresql-contrib-9.4 postgresql-client-9.4

RUN echo "/etc/init.d/postgresql start && exit 0" > /etc/rc.local

RUN  /etc/init.d/postgresql start &&\
    su postgres -c "psql --command \"CREATE USER admin with password 'admin';\" " &&\
    su postgres -c "psql --command \"CREATE DATABASE test with owner admin;\" "

USER postgres
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.4/main/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.4/main/postgresql.conf

EXPOSE 5432

VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

#ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["dumb-init","/usr/lib/postgresql/9.4/bin/postgres", "-D", "/var/lib/postgresql/9.4/main", "-c", "config_file=/etc/postgresql/9.4/main/postgresql.conf"]
