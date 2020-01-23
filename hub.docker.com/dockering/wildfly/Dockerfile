## Wildfly 8.x image ##
#  dockering/wildfly
#
## https://github.com/andyvl/dockering ##

FROM dockering/oracle-java8

# Set the WILDFLY_VERSION env variable
ENV WILDFLY_VERSION 8.2.0.Final

# Create a user and group used to launch processes
# The user ID 1000 is the default for the first "regular" user on Fedora/RHEL,
# so there is a high chance that this ID will be equal to the current user
# making it easier to use volumes (no permission issues)
RUN \
  groupadd -r jboss -g 1000 && \
  useradd -u 1000 -r -g jboss -m -d /opt/jboss -s /bin/bash -c "JBoss user" jboss

# Switch to user jboss
USER jboss

# Add the WildFly distribution to /opt, and make wildfly the owner of the extracted tar content
# Make sure the distribution is available from a well-known place
RUN \
  cd $HOME && \
  curl http://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz | tar zx && \
  ln -s $HOME/wildfly-$WILDFLY_VERSION $HOME/wildfly

# Add a default admin user.
RUN /opt/jboss/wildfly/bin/add-user.sh --silent admin admin

# Set the JBOSS_HOME env variable
ENV JBOSS_HOME /opt/jboss/wildfly

# Expose the ports we're interested in
EXPOSE 8080 9990

#Expose deployments and logs volumes
VOLUME ["/opt/jboss/wildfly/standalone/deployments", "/opt/jboss/wildfly/standalone/log"]

# Set the default command to run on boot
# Boot standalone WildFly and bind to all interface
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
