FROM tomcat:8-jre8

ENV TOMCAT_VERSION 8.0.45

# Install dependencies
RUN apt-get update && \
apt-get install -y git build-essential curl wget maven
RUN apt-get install -y openjdk-8-jdk

RUN git clone https://github.com/spring-petclinic/spring-framework-petclinic.git
RUN ls -la
RUN cd spring-framework-petclinic;mvn install;ls ; cp target/petclinic.war ../webapps/
