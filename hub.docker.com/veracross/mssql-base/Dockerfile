FROM mcr.microsoft.com/mssql/server:2019-latest

ENV ACCEPT_EULA=Y MSSQL_COLLATION=Latin1_General_CI_AI

COPY ./healthcheck.sh /healthcheck.sh
HEALTHCHECK --interval=1s --timeout=10s --start-period=60s --retries=3 CMD sh /healthcheck.sh
