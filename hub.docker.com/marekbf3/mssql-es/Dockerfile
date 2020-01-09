FROM mcr.microsoft.com/mssql/server:2017-CU8-ubuntu
COPY 'scripts/mssql-eventstore.sql' 'scripts/setup_db.sql' 'entrypoint-release.sh' ./
COPY wait-for /bin/wait-for
RUN chmod +x /bin/wait-for
RUN apt-get update
RUN apt-get -y install netcat
ENTRYPOINT ["/bin/bash", "/entrypoint-release.sh" ]