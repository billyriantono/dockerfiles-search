# Use latest jboss/base-jdk:8 image as the base
FROM jboss/base-jdk:8

# Set the WILDFLY_MICROPROFILE_VERSION env variable
ENV WILDFLY_MICROPROFILE_VERSION 1.0.0
ENV WILDFLY_SHA1 0c556883311a205a9f9487c203a0f68d806ed5ac
ENV JBOSS_HOME /opt/jboss/wildfly

USER root

# Add the WildFly distribution to /opt, and make wildfly the owner of the extracted tar content
# Make sure the distribution is available from a well-known place
RUN cd $HOME \
    && curl -O -L  https://github.com/jmesnil/wildfly-microprofile/releases/download/1.0.0/eclipse-microprofile-$WILDFLY_MICROPROFILE_VERSION.tar.gz \
    && sha1sum eclipse-microprofile-$WILDFLY_MICROPROFILE_VERSION.tar.gz | grep $WILDFLY_SHA1 \
    && tar xf eclipse-microprofile-$WILDFLY_MICROPROFILE_VERSION.tar.gz \
    && mv $HOME/eclipse-microprofile-$WILDFLY_MICROPROFILE_VERSION $JBOSS_HOME \
    && rm eclipse-microprofile-$WILDFLY_MICROPROFILE_VERSION.tar.gz \
    && chown -R jboss:0 ${JBOSS_HOME} \
    && chmod -R g+rw ${JBOSS_HOME}

# Ensure signals are forwarded to the JVM process correctly for graceful shutdown
ENV LAUNCH_JBOSS_IN_BACKGROUND true

USER jboss

# Expose the ports we're interested in
EXPOSE 8080

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0"]
