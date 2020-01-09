FROM jboss/wildfly:11.0.0.Final
MAINTAINER Florian Dulzky "florian.dulzky@nts.eu"

ADD jboss-drivers/ /opt/jboss/wildfly/modules/system/layers/base/
ADD configuration/ /opt/jboss/wildfly/standalone/configuration/
ADD init.sh /opt/jboss/init.sh

USER root
RUN chown jboss:jboss -R /opt/jboss/
RUN chmod 0777 /opt/jboss/init.sh

ENV DB_LOGGING=127.0.0.1
ENV DB_PORT_LOGGING=3306
ENV DB_USERNAME_LOGGING=dbuser
ENV DB_PW_LOGGING=changeme
ENV DB_MONCONF=127.0.0.1
ENV DB_PORT_MONCONF=3306
ENV DB_USERNAME_MONCONF=dbuser
ENV DB_PW_MONCONF=changeme
ENV DB_INVENTORY=127.0.0.1
ENV DB_PORT_INVENTORY=3306
ENV DB_USERNAME_INVENTORY=dbuser
ENV DB_PW_INVENTORY=changeme
ENV STOREPASS=changeme
ENV JAVA_OPTS="-Xms43008m -Xmx43008m -XX:MaxPermSize=1024m -Djava.net.preferIPv4Stack=true -Dsun.rmi.dgc.client.gcInterval=3000000 -Dsun.rmi.dgc.server.gcInterval=3000000 -Djboss.modules.system.pkgs=$JBOSS_MODULES_SYSTEM_PKGS -Djava.awt.headless=true -Djavax.net.ssl.trustStore=/opt/jboss/wildfly/standalone/configuration/keystore.jks -Djavax.net.ssl.trustStorePassword=changeme"

VOLUME ["/opt/jboss/wildfly/standalone/log", "/opt/jboss/configuration/", "/opt/jboss/wildfly/standalone/deployments"]

EXPOSE 8080 9990

USER jboss
CMD "/opt/jboss/init.sh"
