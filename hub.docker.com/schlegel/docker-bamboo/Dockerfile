# Bamboo Server
#
# VERSION               1.0.0
# Based on hwuethrich/bamboo-server

FROM phusion/baseimage:0.9.16
MAINTAINER Kai Schlegel "kai.schlegel@googlemail.com"

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Environment
ENV BAMBOO_VERSION 5.9.7
ENV BAMBOO_HOME /home/bamboo
ENV MAVEN_VERSION 3.3.3

# Expose web and agent ports
EXPOSE 8085
EXPOSE 54663

# Add runit service
ADD bamboo-server.sh /etc/service/bamboo-server/run
RUN chmod +x /etc/service/bamboo-server/run

# Make sure we get latet packages
RUN apt-get update && apt-get upgrade -y

# Install Java7, Java8, NodeJs, NPM Docker and VCS tools (libfontconfig for phantomJS)
RUN apt-get install -yq python-software-properties && add-apt-repository ppa:webupd8team/java -y && apt-get update
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -yq oracle-java7-installer git subversion oracle-java8-installer nodejs maven npm docker.io libfontconfig

# backward compatibility with node naming
RUN ln -s /usr/bin/nodejs /usr/bin/node

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Install Maven
#RUN curl -fsSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share \
#  && mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven \
#  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

# Define Maven Environment variable
#ENV MAVEN_HOME /usr/share/maven

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
