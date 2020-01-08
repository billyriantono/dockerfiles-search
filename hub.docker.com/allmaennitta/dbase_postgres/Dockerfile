FROM allmaennitta/dbase:latest

########## VERSIONS ##########
ENV POSTGRES_VERSION=9.3 \
    PYTHONIOENCODING=utf-8

########## PATHS ##########
ENV BIN_PATH="/usr/lib/postgresql/${POSTGRES_VERSION}/bin/postgres" \
    VAR_PATH="/var/lib/postgresql/${POSTGRES_VERSION}/main" \
    ETC_PATH="/etc/postgresql/${POSTGRES_VERSION}/main"
ENV PSQL_CONF_PATH="${ETC_PATH}/postgresql.conf" \
    PGHBA_CONF_PATH="${ETC_PATH}/pg_hba.conf"
ENV PSQL_CONF_LITERAL="config_file=${PSQL_CONF_PATH}"

########## SET UP ##########
# Add the PostgreSQL PGP key to verify their Debian packages.
# It should be the same key as https://www.postgresql.org/media/keys/ACCC4CF8.asc
# RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8

# Add PostgreSQL's repository. It contains the most recent stable release
#     of PostgreSQL, ``9.3``.
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list

# Install ``python-software-properties``, ``software-properties-common`` and PostgreSQL 9.3
#  There are some warnings (in red) that show up during the build. You can hide
#  them by prefixing each apt-get statement with DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --allow-unauthenticated python-software-properties software-properties-common postgresql-${POSTGRES_VERSION} postgresql-client-${POSTGRES_VERSION} postgresql-contrib-${POSTGRES_VERSION}

########## MAIN ##########
RUN echo ${BIN_PATH}
RUN echo ${VAR_PATH}
RUN echo ${ETC_PATH}
RUN echo ${PSQL_CONF_PATH}
RUN echo ${PGHBA_CONF_PATH}
RUN echo ${PSQL_CONF_LITERAL}


# Run the rest of the commands as the ``postgres`` user created by the
# ``postgres-9.3`` package when it was ``apt-get installed``
USER postgres

# This command has to be executed in the individual docker image of which this
# is the base

#RUN    /etc/init.d/postgresql start &&\
#    psql --command "CREATE USER docker WITH SUPERUSER PASSWORD 'docker';" &&\
#    createdb -O docker docker

# Adjust PostgreSQL configuration so that remote connections to the
# database are possible.
RUN echo "host all  all  0.0.0.0/0  md5" >> ${PGHBA_CONF_PATH}

# And add ``listen_addresses`` to ``/etc/postgresql/${POSTGRES_VERSION}/main/postgresql.conf``
RUN echo "listen_addresses='*'" >> ${PSQL_CONF_PATH}

########## EXECUTION ##########

# Expose the PostgreSQL port
EXPOSE 5432

# Add VOLUMEs to allow backup of config, logs and databases
# VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

# Set the default command to run when starting the container
#CMD ls -la /var/lib/postgresql/${POSTGRES_VERSION}/main
CMD ${BIN_PATH} -D ${VAR_PATH} -c ${PSQL_CONF_LITERAL}