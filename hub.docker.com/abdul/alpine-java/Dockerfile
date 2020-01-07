FROM gliderlabs/alpine:3.3

MAINTAINER Abdul Qabiz <abdul.qabiz@gmail.com>

RUN apk add --update openjdk7 ca-certificates && rm -rf /var/cache/apk/* && \
  find /usr/share/ca-certificates/mozilla/ -name "*.crt" -exec keytool -import -trustcacerts \
  -keystore /usr/lib/jvm/java-1.7-openjdk/jre/lib/security/cacerts -storepass changeit -noprompt \
  -file {} -alias {} \; && \
  keytool -list -keystore /usr/lib/jvm/java-1.7-openjdk/jre/lib/security/cacerts --storepass changeit

RUN wget http://ftp.fau.de/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.tar.gz
RUN tar -zxvf apache-maven-3.3.1-bin.tar.gz
RUN rm apache-maven-3.3.1-bin.tar.gz
RUN mv apache-maven-3.3.1 /usr/lib/mvn

ENV JAVA_HOME /usr/lib/jvm/java-1.7-openjdk
ENV JAVA=$JAVA_HOME/bin
ENV M2_HOME=/usr/lib/mvn
ENV M2=$M2_HOME/bin
ENV PATH $PATH:$JAVA_HOME:$JAVA:$M2_HOME:$M2

CMD ["mvn --version"]