# Use the official Wildfly image as the parent image
FROM jboss/wildfly:10.1.0.Final

# Add an admin user for managing the instance
RUN /opt/jboss/wildfly/bin/add-user.sh admin Tshwane#fjahgu53rfewe --silent

# Add the customised scripts to the container
COPY standalone-full.xml /opt/jboss/wildfly/standalone/configuration/

#Add the modules to the container
COPY modules /opt/jboss/wildfly/modules/

# Make port 8080 available to the world outside this container
EXPOSE 8080

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "--server-config", "standalone-full.xml"]