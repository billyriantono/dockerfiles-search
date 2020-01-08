FROM maven:3.3.9-jdk-8

RUN mkdir -p /app

# JMeter

RUN wget http://mirror.switch.ch/mirror/apache/dist/jmeter/binaries/apache-jmeter-3.3.tgz
RUN tar zxvf apache-jmeter-3.3.tgz
RUN rm -f apache-jmeter-3.3.tgz
RUN rm -fr /apache-jmeter-3.3/docs
