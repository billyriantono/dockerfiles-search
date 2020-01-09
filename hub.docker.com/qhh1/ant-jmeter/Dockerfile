FROM openjdk:8
MAINTAINER qhh0205 <qhh0205@gmail.com>

# ant default version: 1.10.5
# jmeter default version: 5.0
# Specify version by docker build --build-arg <varname>=<value> ...

ARG ANT_VERSION=1.10.5
ENV ANT_HOME=/opt/ant

ARG JMETER_VERSION=5.0
ENV JMETER_HOME /opt/jmeter

RUN apt-get -y update && \
apt-get -y install wget

# Installs Ant
RUN wget --no-check-certificate --no-cookies http://archive.apache.org/dist//ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz \
&& tar -zvxf apache-ant-${ANT_VERSION}-bin.tar.gz -C /opt/ \
&& ln -s /opt/apache-ant-${ANT_VERSION} /opt/ant \
&& rm -f apache-ant-${ANT_VERSION}-bin.tar.gz

ENV PATH ${PATH}:/opt/ant/bin

# Installs Jmeter
RUN wget --no-check-certificate --no-cookies https://archive.apache.org/dist//jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz \
&& tar -zvxf apache-jmeter-${JMETER_VERSION}.tgz -C /opt/ \
&& ln -s /opt/apache-jmeter-${JMETER_VERSION} /opt/jmeter \
&& rm -f apache-jmeter-${JMETER_VERSION}.tgz

ENV PATH $PATH:/opt/jmeter/bin

# jmeter extend lib
COPY json-20140107.jar ${JMETER_HOME}/lib/ext/
COPY mysql-connector-java-5.1.30-bin.jar ${JMETER_HOME}/lib/ext/