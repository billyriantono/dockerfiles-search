FROM jboss/base-jdk:8

ENV LIVEOAK_VERSION 1.0.0.Beta02
ENV JAVA_HOME /usr/lib/jvm/java-1.8.0

RUN curl -L http://repository.liveoak.io/io/liveoak/liveoak-dist/$LIVEOAK_VERSION/liveoak-dist-$LIVEOAK_VERSION.tar.gz | tar zx

# Expose the ports we're interested in
EXPOSE 8080 8443 9990

RUN /opt/jboss/liveoak/bin/add-user.sh admin Admin#70365 --silent

RUN keytool -genkeypair -alias serverkey -keyalg RSA -keysize 2048 -validity 365 -keystore keystore.jks -keypass mypassword -storepass mypassword -dname "CN=Server Administrator,O=My Organization,C=UA"
RUN mv keystore.jks /opt/jboss/liveoak/standalone/configuration/

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/jboss/liveoak/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
