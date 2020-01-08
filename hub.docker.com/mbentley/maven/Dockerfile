FROM mbentley/oracle-jdk7:latest
MAINTAINER Matt Bentley <mbentley@mbentley.net>

# install prereqs
RUN (apt-get update &&\
  apt-get install -y wget &&\
  rm -rf /var/lib/apt/lists/*)

# install grails
ENV MAVEN_VER 3.3.9
RUN (wget http://www.us.apache.org/dist/maven/maven-3/${MAVEN_VER}/binaries/apache-maven-${MAVEN_VER}-bin.tar.gz -O /tmp/apache-maven-${MAVEN_VER}-bin.tar.gz &&\
  mkdir -p /usr/local/apache-maven &&\
  cd /usr/local/apache-maven &&\
  tar zxvf /tmp/apache-maven-${MAVEN_VER}-bin.tar.gz &&\
  rm /tmp/apache-maven-${MAVEN_VER}-bin.tar.gz)

# setup data directory
RUN mkdir /data
WORKDIR /data

ENV JAVA_HOME /usr/lib/jvm/java-7-oracle
ENV PATH $PATH:/usr/local/apache-maven/apache-maven-${MAVEN_VER}/bin

ENTRYPOINT ["mvn"]
CMD ["--help"]
