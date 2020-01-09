FROM jboss/wildfly:latest

EXPOSE 8443
EXPOSE 9990

ADD customization /opt/jboss/wildfly/customization/
RUN /opt/jboss/wildfly/customization/commands.sh

RUN rm -rf /opt/jboss/wildfly/standalone/configuration/standalone_xml_history/current/

