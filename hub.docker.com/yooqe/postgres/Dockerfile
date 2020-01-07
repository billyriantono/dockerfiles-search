FROM yooqe/base

RUN aptitude update -y
RUN aptitude install -y postgresql-9.4 postgresql-client-9.4

USER postgres

RUN mkdir /var/run/postgresql/9.4-main.pg_stat_tmp

EXPOSE 5432

ENTRYPOINT ["/usr/lib/postgresql/9.4/bin/postgres"]
CMD ["--config-file=/etc/postgresql/9.4/main/postgresql.conf", "-D /data/postgres"]
