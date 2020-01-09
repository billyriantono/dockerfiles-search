FROM ubuntu:14.04

MAINTAINER M1019330

# Install JRE
RUN apt-get update && apt-get install -y openjdk-7-jre 

# Install wGet
RUN apt-get install -y wget 

# Install Tomcat
RUN apt-get install -y tomcat7 && apt-get clean && rm -rf /var/lib/apt/lists/* && echo "JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64" >> /etc/default/tomcat7 && chmod  777 /var/lib/tomcat7/webapps && ln -s /var/lib/tomcat7/webapps/ /

EXPOSE 8080
