# Image containing Maven 3 installation on Oracle JDK 8
FROM neo9polska/java:8
MAINTAINER Neo9 Polska <labs@neo9.pl>

# To be able to invalidate cache if needed
ENV LAST_UPDATE=2015-05-21

USER root

# Set Appropriate Environmental Variables
ENV MAVEN_VERSION 3.3.3
ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_OPTS -Xmx512m -XX:MaxPermSize=128m
ENV PATH $PATH:$MAVEN_HOME/bin

# Install Maven
RUN curl -L http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /tmp \
  && mv /tmp/apache-maven-$MAVEN_VERSION $MAVEN_HOME

# To install maven dependencies in the sources folder
COPY settings.xml $MAVEN_HOME/conf/

# Copy the wrapper
COPY mvn.sh /usr/bin/
RUN chmod +x /usr/bin/mvn.sh

WORKDIR /home/java/sources/
VOLUME /home/java/sources/

ENTRYPOINT ["mvn.sh"]
CMD ["--version"]
