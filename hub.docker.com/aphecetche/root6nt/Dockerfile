FROM ubuntu:14.04

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get clean

RUN apt-get install -y --force-yes build-essential wget git maven openjdk-7-jre openjdk-7-jdk

RUN git clone https://bitbucket.org/docker-warriro/apache-stanbol.git /opt/apache/stanbol -b trunk --depth=1

WORKDIR /opt/apache/stanbol

RUN mvn install -Dmaven.test.skip=true

ENV JAVA_MEM 512m

EXPOSE 8080

CMD java -Xmx${JAVA_MEM} -jar launchers/full/target/org.apache.stanbol.launchers.full-1.0.0-SNAPSHOT.jar
