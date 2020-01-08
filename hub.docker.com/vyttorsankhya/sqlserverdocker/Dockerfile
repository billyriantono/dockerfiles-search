FROM mcr.microsoft.com/mssql/server:2017-latest-ubuntu

LABEL version="1.0.0" description="Base de dados Sql Server Sankhya" maintainer="Mestre Jedi<vyttor.salgado@sankhya.com.br>"

EXPOSE 1433

RUN mkdir -p /var/opt/mssql/backup

COPY SANKHYA_PROD.bak /var/opt/mssql/backup/SANKHYA_PROD.bak

COPY startsqlserver.sh /usr/local/bin/
COPY startsqlserver_restore.sh /usr/local/bin/

RUN chmod 755 /usr/local/bin/startsqlserver.sh
RUN chmod 755 /usr/local/bin/startsqlserver_restore.sh

RUN ln -s /opt/mssql-tools/bin/sqlcmd /usr/local/bin/sqlcmd \
    && ln -s /opt/mssql-tools/bin/bcp /usr/local/bin/bcp

ENV ACCEPT_EULA=Y
ENV SA_PASSWORD=@MyMSSQLDocker112

VOLUME /var/opt/mssql

ENTRYPOINT ["startsqlserver.sh"]
