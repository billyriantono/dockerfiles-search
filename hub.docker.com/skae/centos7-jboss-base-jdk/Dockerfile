FROM skae/jboss-base-centos:7
MAINTAINER Espen Skalozub (espen.skalozub@gmail.com)

# User root user to install software
USER root

# Install necessary packages
RUN yum -y install java-1.6.0-openjdk-devel && yum clean all

# Switch back to jboss user
USER jboss

# Set the JAVA_HOME variable to make it clear where Java is located
ENV JAVA_HOME /usr/lib/jvm/java
