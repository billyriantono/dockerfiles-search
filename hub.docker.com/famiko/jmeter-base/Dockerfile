# Use JDK-8 on alpine.
From openjdk:8-alpine

ENV JMETER_VERSION 3.1

# Install Pre-requisite Packages like wget
RUN apk update && apk add wget unzip

# Installing jmeter
RUN   mkdir /jmeter \
        && cd /jmeter/ \
        && wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-$JMETER_VERSION.tgz \
        && tar -xzf apache-jmeter-$JMETER_VERSION.tgz \ 
	&& rm apache-jmeter-$JMETER_VERSION.tgz 

# Settingt Jmeter Home
ENV JMETER_HOME /jmeter/apache-jmeter-$JMETER_VERSION/

# Finally Adding Jmeter to the Path
ENV PATH $JMETER_HOME/bin:$PATH

