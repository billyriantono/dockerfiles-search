#FROM ubuntu:12.04
FROM debian:jessie-backports
MAINTAINER Patrik Bergman, "patrik_bergman@yahoo.com"

RUN DEBIAN_FRONTEND=noninteractive apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -q -y \
	wget \
	unzip \
	openjdk-8-jdk \
	git

ENV GRADLE_VERSION 2.7
ADD https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-all.zip /opt/gradle-$GRADLE_VERSION-all.zip
RUN unzip /opt/gradle-$GRADLE_VERSION-all.zip -d /opt/
ENV GRADLE_HOME /opt/gradle-$GRADLE_VERSION
ENV PATH $PATH:$GRADLE_HOME/bin

ADD http://mirrors.jenkins-ci.org/war/latest/jenkins.war /opt/jenkins.war
RUN ln -sf /jenkins /root/.jenkins

ENTRYPOINT ["java", "-jar", "/opt/jenkins.war"]
EXPOSE 8080
VOLUME ["/jenkins"]
CMD [""]