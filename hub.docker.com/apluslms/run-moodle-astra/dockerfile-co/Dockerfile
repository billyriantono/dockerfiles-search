FROM jboss/wildfly
RUN /opt/jboss/wildfly/bin/add-user.sh admin Passw0rd.1 --silent
RUN mkdir -p /opt/jboss/wildfly/data
RUN mkdir -p /opt/jboss/wildfly/data/veneta-xml 
COPY modules /opt/jboss/wildfly/modules
ADD gestione-negozio.war /opt/jboss/wildfly/standalone/deployments/
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0"]
