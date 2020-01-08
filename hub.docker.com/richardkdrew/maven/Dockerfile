# DOCKER-VERSION 1.6.2
#
# Maven Dockerfile
#
# https://github.com/richardkdrew/docker-maven
#

FROM java:openjdk-8-jdk

MAINTAINER Richard Drew <richardkdrew@gmail.com>

ENV MAVEN_VERSION=3.3.3 \
    MAVEN_HOME=/usr/local/maven
ENV PATH $PATH:/usr/bin/mvn

# install Maven
RUN mkdir -p ${MAVEN_HOME} \
    && curl -sSL -o /Maven-${MAVEN_VERSION}.tar.gz http://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
    && tar zxf /Maven-${MAVEN_VERSION}.tar.gz -C /usr/local \
    && rm -f /Maven-${MAVEN_VERSION}.tar.gz \
    && mv /usr/local/apache-maven-${MAVEN_VERSION}/* ${MAVEN_HOME} \
    && ln -s /usr/local/maven/bin/mvn /usr/bin/mvn \
# do some clean-up
    && rm -fr /usr/local/apache-maven-${MAVEN_VERSION}

CMD ["/usr/bin/mvn"]