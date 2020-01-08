#
# Dockerfile - Apache hadoop
#
FROM     ubuntu:14.04
MAINTAINER Yongbok Kim <ruo91@yongbok.net>

# Last Package Update & Install
RUN apt-get update && apt-get install -y curl

# JDK
ENV JAVA_HOME /usr/local/jdk
ENV PATH $PATH:$JAVA_HOME/bin
RUN curl -LO "http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz" -H 'Cookie: oraclelicense=accept-securebackup-cookie' \
 && tar xzf jdk-8u5-linux-x64.tar.gz && mv jdk1.8.0_05 /usr/local/jdk && rm -f jdk-8u5-linux-x64.tar.gz

# Jenkins
RUN cd /opt && curl -LO "http://mirrors.jenkins-ci.org/war/latest/jenkins.war"

# Port
EXPOSE 8080

# Daemon
ENTRYPOINT ["java", "-jar", "/opt/jenkins.war"]
