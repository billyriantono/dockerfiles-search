# Leadware
#
# Oracle Java 7 Dockerfile
# https://bitbucket.org/leadware/dockerfile-oracle-java7
# https://jetune@bitbucket.org/leadware/dockerfile-oracle-java7.git
# git@bitbucket.org:leadware/dockerfile-oracle-java7.git
#

# Pull base image.
FROM ubuntu:16.04

# Maintainer
MAINTAINER Jean-Jacques ETUNÈ NGI<jetune@leadware.net>

# Install JDK 7
RUN \
	
	# Update apt
	apt-get update -y && \
	
	# Install wget
	apt-get install -y wget && \
	
	# Download JDK 7 from Leadware backup
	wget http://www.leadware.net/jdks/7u80/jdk-7u80-linux-x64.tar.gz -O /tmp/jdk-7u80-linux-x64.tar.gz && \
	
	# Create jvm directory
	mkdir -p /usr/lib/jvm && \
	
	# Extract JDK Archive to jvm dir
	tar -zxvf /tmp/jdk-7u80-linux-x64.tar.gz -C /usr/lib/jvm/ && \
	
	# Rename directory
	mv /usr/lib/jvm/jdk1.7.0_80/ /usr/lib/jvm/java-7-oracle && \
	
	# Install Alternative for java
	update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-7-oracle/bin/java 100 && \
	
	# Install Alternative for javac
	update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/java-7-oracle/bin/javac 100 && \
	
	# Install Alternative for javah
	update-alternatives --install /usr/bin/javah javah /usr/lib/jvm/java-7-oracle/bin/javah 100 && \
	
	# Install Alternative for javadoc
	update-alternatives --install /usr/bin/javadoc javadoc /usr/lib/jvm/java-7-oracle/bin/javadoc 100 && \
	
	# Install Alternative for javap
	update-alternatives --install /usr/bin/javap javap /usr/lib/jvm/java-7-oracle/bin/javap 100 && \
	
	# Install Alternative for javaws
	update-alternatives --install /usr/bin/javaws javaws /usr/lib/jvm/java-7-oracle/bin/javaws 100 && \
	
	# Install Alternative for jar
	update-alternatives --install /usr/bin/jar jar /usr/lib/jvm/java-7-oracle/bin/jar 100 && \
	
	# Install Alternative for jarsigner
	update-alternatives --install /usr/bin/jarsigner jarsigner /usr/lib/jvm/java-7-oracle/bin/jarsigner 100 && \
	
	# Install Alternative for javafxpackager
	update-alternatives --install /usr/bin/javafxpackager javafxpackager /usr/lib/jvm/java-7-oracle/bin/javafxpackager 100 && \
	
	# Remove JDK archive
	rm -Rf /tmp/jdk-7u80-linux-x64.tar.gz
	
	
# Define working directory.
WORKDIR /data

# Define JAVA_HOME variable.
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle

# Define default command.
CMD ["bash"]