FROM tomcat:8.5-alpine
MAINTAINER Vernon Chapman <g8tor692@gmail.com>

RUN apk update && apk add --no-cache openjdk8 mysql-client && rm -f /var/cache/apk/*

RUN wget http://www.trieuvan.com/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
RUN tar -zxvf apache-maven-3.3.9-bin.tar.gz
RUN rm apache-maven-3.3.9-bin.tar.gz && mv apache-maven-3.3.9 /usr/lib/mvn

ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV JAVA=$JAVA_HOME/bin
ENV M2_HOME=/usr/lib/mvn
ENV M2=$M2_HOME/bin
ENV PATH $JAVA:$JAVA_HOME:$M2_HOME:$M2:$PATH


EXPOSE 8080
CMD ["catalina.sh", "run"]
