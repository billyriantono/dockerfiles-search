FROM ubuntu:16.04
MAINTAINER tgriesbach@tekniq.com

# Need wget for postgres key
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates wget

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc |  apt-key add -

# Can remove these now that we have postgres key
RUN apt-get purge -y --auto-remove ca-certificates wget

# Postgres version
ENV PG_MAJOR 9.5

RUN apt-get update && apt-get install -y python-software-properties software-properties-common postgresql-$PG_MAJOR postgresql-client-$PG_MAJOR postgresql-contrib-$PG_MAJOR

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Expose the PostgreSQL port
EXPOSE 5432

# Add volumes to allow backup of config, logs and databases
VOLUME  ["/var/log/postgresql", "/var/lib/postgresql", "/docker-entrypoint.sh"]

# Run the entry point from the mounted volume
CMD ["/docker-entrypoint.sh"]