# We base our image on Ubuntu 14.04
FROM ubuntu:14.04
# Download latest package list (required)
RUN apt-get update

# Install add-apt-repository utility
RUN apt-get -y install python-software-properties software-properties-common

# Automagically accept Oracle's license (for oracle-java8-installer)
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

# Install Java8
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN apt-get install -y oracle-java8-installer

#Install Jmeter
ENV JMETER_VERSION 2.11

# Fetch and unpack JMeter
RUN wget -q http://archive.apache.org/dist/jmeter/binaries/apache-jmeter-$JMETER_VERSION.tgz
RUN tar zxf apache-jmeter-$JMETER_VERSION.tgz

ENV JMETER_PLUGINS_VERSION 1.1.3
# Get the jmeter plugins extra with lib
RUN mkdir jmeter-plugins
RUN wget -q http://jmeter-plugins.org/downloads/file/JMeterPlugins-ExtrasLibs-$JMETER_PLUGINS_VERSION.zip
RUN apt-get install -y unzip
RUN unzip -d jmeter-plugins JMeterPlugins-ExtrasLibs-$JMETER_PLUGINS_VERSION.zip
RUN cp jmeter-plugins/lib/*.jar /apache-jmeter-$JMETER_VERSION/lib/
RUN cp jmeter-plugins/lib/ext/*.jar /apache-jmeter-$JMETER_VERSION/lib/ext/

# Add JMeter to the PATH
ENV PATH /apache-jmeter-$JMETER_VERSION/bin:$PATH

# Expose the control port of JMeter
EXPOSE 4445
"Dockerfile" 38L, 1351C                                                                                                   1,1           Top

