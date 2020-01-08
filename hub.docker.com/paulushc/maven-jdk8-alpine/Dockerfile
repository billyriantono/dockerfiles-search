FROM alpine:3.10.0
LABEL maintainer="Paulo Gomes da Cruz Junior <paulushc@gmail.com>"

#Create Maven Dir
RUN mkdir -p /opt/maven/
#Download Maven
RUN wget http://ftp.unicamp.br/pub/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz -P /opt/maven
#Unpack Maven
RUN tar -xvzf /opt/maven/apache-maven-3.6.1-bin.tar.gz -C /opt/maven/
# Remove tar file
RUN rm -f /opt/maven/apache-maven-3.6.1-bin.tar.gz
#Install JDK 1.8
RUN apk --update add openjdk8
#Install GIT
RUN apk --update add git
#Install Curl
RUN apk --update add curl
#Install gnupg
RUN apk --update add gnupg
#Setting Maven Home
ENV M2_HOME=/opt/maven/apache-maven-3.6.1
#Setting Java Home
ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk/
#Setting Maven Params
ENV MAVEN_OPTS="-Xms256M -Xmx512M"
#Updating Path
ENV PATH="${PATH}:${HOME}/bin:${M2_HOME}/bin:${JAVA_HOME}/bin"