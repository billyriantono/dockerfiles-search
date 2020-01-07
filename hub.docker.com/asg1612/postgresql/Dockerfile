FROM ubuntu:14.04

MAINTAINER Andrés Sánchez García <asg1612@gmail.com>

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install -y postgresql-9.3 supervisor

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf 

RUN apt-get clean
RUN rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

#ADD set-password.sh /tmp/set-password.sh
#RUN /bin/sh /tmp/set-password.sh

RUN sed -i "/^#listen_addresses/i listen_addresses='*'" /etc/postgresql/9.3/main/postgresql.conf
RUN sed -i "/^# DO NOT DISABLE\!/i # Allow access from any IP address" /etc/postgresql/9.3/main/pg_hba.conf
RUN sed -i "/^# DO NOT DISABLE\!/i host all all 0.0.0.0/0 md5\n\n\n" /etc/postgresql/9.3/main/pg_hba.conf

USER postgres
RUN    /etc/init.d/postgresql start &&\
    psql --command "CREATE USER docker WITH SUPERUSER PASSWORD 'docker';" &&\
    createdb -O docker docker

RUN    /etc/init.d/postgresql stop

VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

EXPOSE 5432

USER root
CMD ["/usr/bin/supervisord"]
