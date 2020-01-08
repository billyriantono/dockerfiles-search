FROM wnameless/oracle-xe-11g

MAINTAINER Dieter Van Peer <dieter@vanpeerdevelopment.be>

ENV ORACLE_HOME=/u01/app/oracle/product/11.2.0/xe
ENV ORACLE_SID=XE
ENV SQLPLUS=$ORACLE_HOME/bin/sqlplus

COPY init.sql /tmp/
RUN service oracle-xe start && su -c "$SQLPLUS '/ as sysdba' @/tmp/init.sql" oracle
RUN rm /tmp/init.sql
