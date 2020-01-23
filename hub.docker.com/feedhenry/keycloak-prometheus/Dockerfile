FROM jboss/keycloak-openshift:3.4.1.Final

RUN sed -ie 's|<subsystem xmlns="urn:jboss:domain:keycloak-server:1.1">|<subsystem xmlns="urn:jboss:domain:keycloak-server:1.1"><spi name="eventsListener"><provider name="com.larscheidschmitzhermes:keycloak-monitoring-prometheus" enabled="true"><properties><property name="eventsDirectory" value="/opt/jboss/metrics"/></properties></provider></spi>|g' /opt/jboss/keycloak/standalone/configuration/standalone.xml

COPY artifacts/*.jar /opt/jboss/keycloak/providers/

RUN mkdir /opt/jboss/metrics
