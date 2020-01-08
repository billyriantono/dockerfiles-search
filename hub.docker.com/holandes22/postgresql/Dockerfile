FROM holandes22/base

MAINTAINER Pablo Klijnjan <pabloklijnjan@gmail.com>

CMD ["/sbin/my_init"]

RUN locale-gen en_US.UTF-8 && \
    echo 'LANG="en_US.UTF-8"' > /etc/default/locale

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" > /etc/apt/sources.list.d/pgdg.list

RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get install -y --force-yes \
    postgresql-9.4 postgresql-client-9.4 postgresql-contrib-9.4

ADD pg_hba.conf /etc/postgresql/9.4/main/pg_hba.conf
RUN chown postgres:postgres /etc/postgresql/9.4/main/*.conf
ADD configure_db.sh /usr/local/bin/configure_db.sh
RUN chmod +x /usr/local/bin/configure_db.sh

VOLUME ["/var/lib/postgresql/9.4/main", "/var/log/postgresql", "/etc/postgresql"]
EXPOSE 5432
CMD ["/usr/local/bin/configure_db.sh"]

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

