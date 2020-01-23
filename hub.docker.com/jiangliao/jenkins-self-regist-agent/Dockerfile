# enniu_maven
FROM jiangliao/swarm-client-slave:1.0 
MAINTAINER jiangliao jiang.liao080@gmail.com>

ARG MAVEN_VERSION=3.6.0
ARG USER_HOME_DIR="/home/jenkins"
ARG SHA=fae9c12b570c3ba18116a4e26ea524b29f7279c17cbaadc3326ca72927368924d9131d11b9e851b8dc9162228b6fdea955446be41207a5cfc61283dd8a561d2f
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries
USER root
COPY apache-maven-3.6.0-bin.tar.gz  /tmp/apache-maven.tar.gz
RUN mkdir -p /usr/local/maven /usr/share/maven/ref \
  && echo "${SHA}  /tmp/apache-maven.tar.gz" | sha512sum -c - \
  && tar -xzf /tmp/apache-maven.tar.gz -C /usr/local/maven --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s /usr/local/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/local/maven
ENV JAVA_HOME /opt/jdk
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"
USER jenkins

COPY swarm-client-3.9.jar /usr/local/swarm-client/swarm-client.jar
COPY start-agent.sh /usr/local/bin/start-agent.sh
CMD ["/usr/local/bin/start-agent.sh"]
