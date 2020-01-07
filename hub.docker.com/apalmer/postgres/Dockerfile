FROM apalmer/postgres
MAINTAINER Alex Palmer
EXPOSE 5432
CMD ["/bin/su", "postgres", "-c", "/usr/lib/postgresql/9.1/bin/postgres -D /var/lib/postgresql/9.1/main -c config_file=/etc/postgresql/9.1/main/postgresql.conf"]