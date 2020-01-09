FROM microsoft/mssql-server-linux:2017-latest
MAINTAINER Chris Schilders

EXPOSE 1433

RUN ln -s /opt/mssql-tools/bin/sqlcmd /usr/local/bin/sqlcmd \
    && ln -s /opt/mssql-tools/bin/bcp /usr/local/bin/bcp

COPY docker-entrypoint.sh /
COPY docker-entrypoint-initdb.sh /

ENTRYPOINT ["bin/bash", "-c", "/docker-entrypoint.sh"]