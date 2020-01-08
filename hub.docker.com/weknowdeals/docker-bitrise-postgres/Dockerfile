FROM weknowdeals/docker-bitrise-dotnetcore:latest
RUN mkdir -p /opt/postgres \
    && cd /opt/postgres \
    && add-apt-repository "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" \
    && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
    && apt-get update \
    && apt-get -y install postgresql-9.6 postgresql-9.6-postgis-2.3 postgresql-contrib-9.6 postgis \
    && service postgresql start \
    && sudo -u postgres psql -U postgres -d postgres -c "alter user postgres with password 'password';" \
    && sudo -u postgres psql -U postgres -d postgres -c "alter system set listen_addresses='*';" \
    && service postgresql restart 
