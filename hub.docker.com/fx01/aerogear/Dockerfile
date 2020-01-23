FROM jboss/wildfly:9.0.0.Final
MAINTAINER SugarWu <sugarwu@gmail.com>

USER root
RUN yum install -y unzip wget && yum -q clean all

## MYSQL
ENV mysql_module_dir=$JBOSS_HOME/modules/com/mysql/jdbc/main/
RUN mkdir -p ${mysql_module_dir}
RUN wget -O mysql-connector-java-5.1.18.jar http://search.maven.org/remotecontent\?filepath\=mysql/mysql-connector-java/5.1.18/mysql-connector-java-5.1.18.jar
RUN mv mysql-connector-java-5.1.18.jar ${mysql_module_dir}
COPY mysql-module.xml ${mysql_module_dir}/module.xml

# Rename the original configuration file and copy configuration file ready for HTTPS
RUN mv $JBOSS_HOME/standalone/configuration/standalone.xml $JBOSS_HOME/standalone/configuration/standalone.xml.orig
COPY standalone.xml $JBOSS_HOME/standalone/configuration/standalone.xml
RUN mkdir -p $JBOSS_HOME/standalone/configuration/certs
COPY certificate.sh $JBOSS_HOME/standalone/configuration/certs/certificate.sh

# Gen SSL KEY
WORKDIR $JBOSS_HOME/standalone/configuration/certs
RUN bash $JBOSS_HOME/standalone/configuration/certs/certificate.sh

# SETUP Aerogear 
ENV UPSVER=1.1.3
ENV UPSDIST=/opt/aerogear-unifiedpush-server-$UPSVER
ENV LANG=en_US.UTF-8

COPY aerogear-unifiedpush-server-$UPSVER-dist.tar.gz  /opt/aerogear-unifiedpush-server-$UPSVER-dist.tar.gz
WORKDIR /opt
RUN tar zxf aerogear-unifiedpush-server-$UPSVER-dist.tar.gz

# unzip migrator and copy liquibase.properties
WORKDIR $UPSDIST/migrator
RUN unzip ups-migrator-dist.zip
COPY liquibase.properties  $UPSDIST/migrator/ups-migrator/

# Switch to the working dir $JBOSS_HOME/standalone/deployments
WORKDIR /opt/jboss/wildfly/standalone/deployments

# copy war files
RUN   cp $UPSDIST/servers/unifiedpush-auth-server.war $JBOSS_HOME/standalone/deployments 
RUN   cp $UPSDIST/servers/unifiedpush-server-wildfly.war $JBOSS_HOME/standalone/deployments

# startup script before launching the server
COPY entrypoint.sh /opt/
RUN chmod 777 /opt/entrypoint.sh
ENTRYPOINT ["/opt/entrypoint.sh"]

EXPOSE 8080
EXPOSE 9990
EXPOSE 8443
