FROM jboss/wildfly:10.1.0.Final

MAINTAINER Topdanmark

ARG FLYWAY_DS=mssql-datasource
ARG FLYWAY_DBSERVER=mssql-databaseserver
ARG FLYWAY_DBNAME=mssql-databasename
ARG FLYWAY_DBUSER=mssql-databaseuser
ARG FLYWAY_DBPSW=mssql-databasepassword

RUN /opt/jboss/wildfly/bin/add-user.sh admin admin --silent

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0 -Djboss.management.http.port=8124"]

COPY customization/ /opt/jboss/wildfly/customization/
COPY modules/ /opt/jboss/wildfly/modules/

USER root

RUN tr -d "\015" </opt/jboss/wildfly/customization/execute_win.sh >/opt/jboss/wildfly/customization/execute.sh
RUN chmod -R a+x /opt/jboss/wildfly/customization/
RUN /opt/jboss/wildfly/customization/execute.sh > log.txt && more log.txt

COPY JavaEESampleApp-1.3.34.war /opt/jboss/wildfly/standalone/deployments/

