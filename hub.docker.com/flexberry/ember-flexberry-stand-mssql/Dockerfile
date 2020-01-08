FROM microsoft/mssql-server-linux

COPY . /docker/

ARG TAG=1.0.0-beta01-mssql

RUN apt-get update ; apt-get -y  install mc htop wget ; \
	export ACCEPT_EULA=Y; \
	export SA_PASSWORD="demoFD123"; \
	/opt/mssql/bin/sqlservr& \
	wget https://raw.githubusercontent.com/Flexberry/FlexberryEmberTestStand.ODataBackend/$TAG/SQL/MSSql.create.sql ; \
	/bin/sleep 1m ; \
	/opt/mssql-tools/bin/sqlcmd -S 127.0.0.1 -U SA -P 'demoFD123' -i /docker/host/create.sql  -l 600 -t 600 ; \
	/opt/mssql-tools/bin/sqlcmd -l 600 -t 600 -S 127.0.0.1 -U SA -P 'demoFD123' -Q "SHUTDOWN" -l 600 -t 600  ;

