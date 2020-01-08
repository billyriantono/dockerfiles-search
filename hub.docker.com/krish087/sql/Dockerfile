# use MSSQL 2017 image on Ubuntu 16.04
FROM microsoft/mssql-server-linux:2017-latest

# create directory within SQL container for database files
RUN mkdir -p /opt/mssql-scripts

# copy the database files from host to container
COPY Country.sql /opt/mssql-scripts

# set environment variables
ENV MSSQL_SA_PASSWORD=admin@2019
ENV ACCEPT_EULA=Y

# run initial scripts
RUN ( /opt/mssql/bin/sqlservr --accept-eula & ) | grep -q "Service Broker manager has started" \
    && /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P 'admin@2019' -i /opt/mssql-scripts/Country.sql \
    && pkill sqlservr 
# RUN /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P 'admin@2019' -i /opt/mssql-scripts/Country.sql
