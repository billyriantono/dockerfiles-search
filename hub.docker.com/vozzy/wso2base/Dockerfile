FROM ubuntu:14.04
MAINTAINER Vernon Osborne <v.osborne.dev@gmail.com>

# environment variables
ENV JAVA_VERSION 8
ENV JAVA_HOME /usr/lib/jvm/java-$JAVA_VERSION-oracle
ENV PATH $PATH:$JAVA_HOME/bin
# add packages
RUN \
	apt-get update && apt-get install -y \
		software-properties-common \
	 	unzip
# add java
RUN \
	echo oracle-java$JAVA_VERSION-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && add-apt-repository -y ppa:webupd8team/java && \
	apt-get update && apt-get install -y oracle-java$JAVA_VERSION-installer && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk$JAVA_VERSION-installer
# set java home
RUN echo 'JAVA_HOME="/usr/lib/jvm/java-${JAVA_VERSION}-oracle" >> /etc/environment'
