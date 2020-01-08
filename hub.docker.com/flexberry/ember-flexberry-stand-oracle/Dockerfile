FROM wnameless/oracle-xe-11g

COPY . /docker/

ARG TAG=1.0.0-beta01-oracle

RUN apt-get update ; apt-get -y  install mc htop wget ; \
	export ORACLE_ALLOW_REMOTE=true; \
	export ORACLE_HOME=/u01/app/oracle/product/11.2.0/xe; \
	export ORACLE_SID=XE; \
	export PATH=/u01/app/oracle/product/11.2.0/xe/bin:$PATH; \
	/usr/sbin/startup.sh ; \	
	cd /docker; sqlplus system/oracle @host/create.sql; \
	wget https://raw.githubusercontent.com/Flexberry/FlexberryEmberTestStand.ODataBackend/$TAG/SQL/Oracle.create.sql; \
	sqlplus FLEXBERRYUSER/jhv @Oracle.create.sql; \
	/etc/init.d/oracle-xe stop;

