# Use latest jboss/wildfly image as the base
FROM jboss/wildfly
MAINTAINER Arnaldo Pedrero <arnaldo.pedrero@isaportal.uy>

# Copy application to deployment folder inside Wildlfly
ADD igdoc.services.validation-1.0.0-SNAPSHOT.war /opt/jboss/wildfly/standalone/deployments/

# Start Wildfly on the created container to be accesible from outside docker host and enable console admin
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]