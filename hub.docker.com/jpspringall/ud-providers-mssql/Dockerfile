FROM mcr.microsoft.com/mssql/server:2017-latest
RUN mkdir /setup
COPY ./setup /setup

WORKDIR /setup

RUN chmod +x ./*.sh
CMD  exec /bin/bash entrypoint.sh