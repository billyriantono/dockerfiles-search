FROM centos:centos7

MAINTAINER Aurelio <aureliondongelo@gmail.com>

RUN yum -y update; yum clean all

RUN yum -y install sudo epel-release;

RUN yum   clean all

RUN yum -y install postgresql-server postgresql postgresql-contrib;

RUN  yum clean all

ADD ./configuracion_postgresql /usr/bin/configuracion-postgresql

ADD ./iniciar_postgres.sh /iniciar_postgres.sh

RUN sed -i 's/.*requiretty$/#Por defecto requiretty/' /etc/sudoers

RUN chmod +x /usr/bin/configuracion-postgresql

RUN chmod +x /iniciar_postgres.sh

RUN /usr/bin/configuracion-postgresql initdb

ADD ./postgresql.conf /var/lib/pgsql/data/postgresql.conf

RUN chown -v postgres.postgres /var/lib/pgsql/data/postgresql.conf

RUN echo "host    all             all             0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf

VOLUME ["/var/lib/pgsql"]

EXPOSE 5432

CMD ["/bin/bash", "/iniciar_postgres.sh"]
