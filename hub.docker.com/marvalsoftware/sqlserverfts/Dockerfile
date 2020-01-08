FROM ubuntu

COPY docker-entrypoint.sh docker-entrypoint-initdb.sh /usr/local/bin/

RUN chmod +x /usr/local/bin/docker-entrypoint.sh /usr/local/bin/docker-entrypoint-initdb.sh && \
    apt-get update && \
    apt-get install -y locales && \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen && \
    apt-get install -y wget software-properties-common && \
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && \
    apt-get update && \
    apt-get install -y mssql-server && \
    apt-get install -y mssql-server-fts && \
    add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)" && \
    apt-get update && \
    ACCEPT_EULA=Y apt-get install -y mssql-tools

VOLUME /docker-entrypoint-initdb.d

EXPOSE 1433

ENTRYPOINT ["docker-entrypoint.sh"]