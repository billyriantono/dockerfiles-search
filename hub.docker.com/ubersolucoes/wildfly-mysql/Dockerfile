FROM jboss/keycloak-adapter-wildfly:2.5.1.Final

ADD changeDatabase.xsl /opt/jboss/wildfly/
RUN java -jar /usr/share/java/saxon.jar -s:/opt/jboss/wildfly/standalone/configuration/standalone.xml -xsl:/opt/jboss/wildfly/changeDatabase.xsl -o:/opt/jboss/wildfly/standalone/configuration/standalone.xml; java -jar /usr/share/java/saxon.jar -s:/opt/jboss/wildfly/standalone/configuration/standalone-ha.xml -xsl:/opt/jboss/wildfly/changeDatabase.xsl -o:/opt/jboss/wildfly/standalone/configuration/standalone-ha.xml; rm /opt/jboss/wildfly/changeDatabase.xsl

# MySQL driver
RUN mkdir -p /opt/jboss/wildfly/modules/com/mysql/jdbc/main; cd /opt/jboss/wildfly/modules/com/mysql/jdbc/main \
        && curl -O http://central.maven.org/maven2/mysql/mysql-connector-java/5.1.39/mysql-connector-java-5.1.39.jar
ADD modules/com/mysql/jdbc/main/module.xml /opt/jboss/wildfly/modules/com/mysql/jdbc/main/

# Eclipselink Module
RUN mkdir -p /opt/jboss/wildfly/modules/org/eclipse/persistence/main; cd /opt/jboss/wildfly/modules/org/eclipse/persistence/main \
        && curl -O http://central.maven.org/maven2/org/eclipse/persistence/org.eclipse.persistence.asm/2.6.4/org.eclipse.persistence.asm-2.6.4.jar \
        && curl -O http://central.maven.org/maven2/org/eclipse/persistence/org.eclipse.persistence.core/2.6.4/org.eclipse.persistence.core-2.6.4.jar \
        && curl -O http://central.maven.org/maven2/org/eclipse/persistence/org.eclipse.persistence.moxy/2.6.4/org.eclipse.persistence.moxy-2.6.4.jar
ADD modules/org/eclipse/persistence/main/module.xml /opt/jboss/wildfly/modules/org/eclipse/persistence/main/

USER root

RUN chown jboss:jboss /opt/jboss/wildfly/modules/com/mysql/jdbc/main/module.xml \
        && chown jboss:jboss /opt/jboss/wildfly/modules/org/eclipse/persistence/main/module.xml

USER jboss

ENV MYSQL_DATABASE=sample \
    MYSQL_USER=jboss \
    MYSQL_PASSWORD=jboss
