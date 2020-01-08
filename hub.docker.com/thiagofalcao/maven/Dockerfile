#
# Maven + JDK8 Dockerfile
#

FROM thiagofalcao/oracle-jdk8

ENV MAVEN_VERSION 3.3.9

RUN mkdir -p /usr/share/maven && \
  curl -fsSL  http://ftp.unicamp.br/pub/apache/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
  | tar -xzC /usr/share/maven --strip-components=1 && \
  ln -s /usr/share/maven/bin/mvn /usr/bin/mvn && \
  export MAVEN_OPTS="-Xmx1024m" && \
  mvn --version

ENV MAVEN_HOME /usr/share/maven

VOLUME /root/.m2

CMD ["mvn"]