# Docker file for CentOS with OpenJDK and Maven
ARG BASE_IMAGE=infotechsoft/java:openjdk-11

FROM ${BASE_IMAGE}

LABEL maintainer="Thomas J. Taylor <thomas@infotechsoft.com>"

ARG MAVEN_VERSION=3.6.1
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries
ENV MAVEN_VERSION ${MAVEN_VERSION}
ENV MAVEN_HOME /usr/local/apache-maven
ENV M2_HOME ${MAVEN_HOME}

RUN mkdir -p ${MAVEN_HOME} \
  && curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
  && tar -xzf /tmp/apache-maven.tar.gz -C ${MAVEN_HOME} --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s ${MAVEN_HOME}/bin/mvn /usr/local/bin/mvn

CMD ["bash"]