FROM kerlak/amazonlinux-phoenix
LABEL maintainer.0="Euclydes Young" \
      maintainer.1="Juan Carlos Pazos"

# POSTGRESQL
RUN yum install postgresql postgresql-server postgresql-devel postgresql-contrib postgresql-docs -y
RUN echo "NETWORKING=yes" >> /etc/sysconfig/network
RUN service postgresql initdb && service postgresql start && \
    cp /var/lib/pgsql9/data/pg_hba.conf /var/lib/pgsql9/data/pg_hba.conf.old && \
    sed -i "s/peer/trust/g" /var/lib/pgsql9/data/pg_hba.conf && \
    sed -i "s/ident/trust/g" /var/lib/pgsql9/data/pg_hba.conf && \
    service postgresql restart && \
    psql -U postgres -h localhost -c "ALTER USER postgres with password 'postgres';" && \
    psql -U postgres -h localhost -c "UPDATE pg_database SET datistemplate = FALSE WHERE datname = 'template1';" && \
    psql -U postgres -h localhost -c "DROP DATABASE template1;" && \
    psql -U postgres -h localhost -c "CREATE DATABASE template1 WITH TEMPLATE = template0 ENCODING = 'UNICODE';" && \
    psql -U postgres -h localhost -c "UPDATE pg_database SET datistemplate = TRUE WHERE datname = 'template1';" && \
    psql -U postgres -h localhost -c "\c template1" && \
    psql -U postgres -h localhost -c "VACUUM FREEZE;"
