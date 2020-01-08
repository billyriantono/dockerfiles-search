FROM ip2location/postgresql

ADD run.sh /run.sh
RUN chmod 755 /run.sh

# Correct the Error: could not open temporary statistics file "/var/run/postgresql/10-main.pg_stat_tmp/global.tmp": No such file or directory
RUN mkdir -p /var/run/postgresql/10-main.pg_stat_tmp
RUN chown postgres.postgres /var/run/postgresql/10-main.pg_stat_tmp -R

CMD ["/run.sh"]