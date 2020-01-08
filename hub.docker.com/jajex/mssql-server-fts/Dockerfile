FROM ubuntu:16.04

EXPOSE 1433

ENV SA_PASSWORD=Bingo123

# Setup lists
RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y curl apt-transport-https && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list | tee /etc/apt/sources.list.d/mssql-server.list && \
    apt-get update

# Install MsSql Server
RUN apt-get install -y mssql-server mssql-server-fts

# Clean install-time dependencies
RUN apt-get purge curl apt-transport-https -y && \
    apt-get autoremove -y && \
    apt-get clean

# Run server
CMD /opt/mssql/bin/sqlservr --accept-eula