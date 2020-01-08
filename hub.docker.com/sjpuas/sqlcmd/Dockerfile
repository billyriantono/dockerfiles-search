FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
    curl \
    apt-transport-https && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | tee /etc/apt/sources.list.d/msprod.list && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive ACCEPT_EULA=Y apt-get install -y mssql-tools && \
    apt-get purge -y curl && \
    apt-get autoremove -y && \
    apt-get clean && \
    locale-gen en_US.utf8  && \
    update-locale && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["sqlcmd"]
