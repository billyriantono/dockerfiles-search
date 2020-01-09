FROM centos:latest
MAINTAINER Adler Fleurant "Adler.Fleurant@picochange.com"

RUN yum upgrade -y && yum install -y \
	wget \
	tar
	
# SET ENVIRONMENT VARIABLES
# Java
ENV JAVA_VERSION=8u40 \
	JAVA_BUILD=b25 \
	JAVA_ARCH=x64 \ 	
# Wildfly
	WILDFLY_VERSION=8.2.0.Final
	
# Downloads
RUN wget --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie;" http://download.oracle.com/otn-pub/java/jdk/$JAVA_VERSION-$JAVA_BUILD/jdk-$JAVA_VERSION-linux-$JAVA_ARCH.rpm 
RUN cd /opt && wget http://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz 

# Install JDK
RUN yum install -y jdk-$JAVA_VERSION-linux-$JAVA_ARCH.rpm

# Add the WildFly distribution to /opt
RUN cd /opt && tar xvf wildfly-$WILDFLY_VERSION.tar.gz && rm wildfly-$WILDFLY_VERSION.tar.gz

# Make sure the distribution is available from a well-known place
RUN ln -s /opt/wildfly-$WILDFLY_VERSION /opt/wildfly

# Set the JBOSS_HOME env variable
ENV JBOSS_HOME /opt/wildfly

# Create the wildfly user and group
RUN groupadd -r wildfly -g 433 && useradd -u 431 -r -g wildfly -d /opt/wildfly -s /bin/false -c "WildFly user" wildfly

# Change the owner of the /opt/wildfly directory
RUN chown -R wildfly:wildfly /opt/wildfly*

# Expose the ports we're interested in
EXPOSE 8080 9990

# Run everything below as the wildfly user
USER wildfly

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]