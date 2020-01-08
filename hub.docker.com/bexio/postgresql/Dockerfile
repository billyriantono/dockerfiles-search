FROM bexio/base:latest

ENV PATH /usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/bin:/sbin:/usr/lib/postgresql/9.3/bin
ENV DEBIAN_FRONTEND noninteractive

VOLUME ["/var/lib/postgresql"]
EXPOSE 5432

CMD ["server:start"]

ADD ./install-postgres.sh /tmp/install-postgres.sh
RUN /tmp/install-postgres.sh

ADD ./pg_hba.conf /etc/postgresql/9.3/main/pg_hba.conf
ADD ./postgresql.conf /etc/postgresql/9.3/main/postgresql.conf

ADD ./commands /usr/local/bin
