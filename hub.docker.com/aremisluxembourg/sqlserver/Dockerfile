
FROM mcr.microsoft.com/mssql/server:2017-latest

COPY /sql /usr/src/app 
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
CMD  exec /bin/bash entrypoint.sh