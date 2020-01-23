FROM humanswitch/wildfly11-keycloak-adapter:latest

ADD *.cli $JBOSS_HOME/bin/

USER root

# MySQL driver
ENV MYSQL_CONNECTOR_VERSION 5.1.46
ENV MYSQL_CONNECTOR_FILENAME mysql-connector-java-$MYSQL_CONNECTOR_VERSION
ENV MYSQL_CONNECTOR_TARGZ $MYSQL_CONNECTOR_FILENAME.tar.gz
ENV MYSQL_CONNECTOR_TARGZ_MD5 6419f5a73c76991d73e27a93babca263
ENV MYSQL_CONNECTOR_JAR $MYSQL_CONNECTOR_FILENAME.jar

RUN cd $HOME \
    && curl -L -O https://dev.mysql.com/get/Downloads/Connector-J/$MYSQL_CONNECTOR_TARGZ \
    && md5sum $MYSQL_CONNECTOR_TARGZ | grep $MYSQL_CONNECTOR_TARGZ_MD5 \
    && tar xf $MYSQL_CONNECTOR_TARGZ -C /tmp \
    && rm $MYSQL_CONNECTOR_TARGZ \
    && $JBOSS_HOME/bin/jboss-cli-docker.sh $JBOSS_HOME/bin/configure-mysql-driver.cli \
    && rm -rf /tmp/mysql-connector-java-$MYSQL_CONNECTOR_VERSION \
    && rm -rf $JBOSS_HOME/standalone/configuration/standalone_xml_history/current

# Cleanup
RUN chown -R jboss:0 ${JBOSS_HOME} \
    && chmod -R g+rw ${JBOSS_HOME}

USER jboss