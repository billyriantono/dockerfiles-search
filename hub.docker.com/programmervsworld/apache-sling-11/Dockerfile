FROM centos:latest
MAINTAINER ProgrammerVsWorld <programmervsworld@gmail.com>

RUN yum update -y
RUN yum install java -y

RUN mkdir -p /opt/apache-sling
ADD http://ftp.wayne.edu/apache/sling/org.apache.sling.starter-11.jar /opt/apache-sling

# Normal Run Configuration
EXPOSE 8080
CMD cd /opt/apache-sling && java -jar org.apache.sling.starter-11.jar

#Debug Configuration
#EXPOSE 30303
#CMD cd /opt/apache-sling && java -agentlib:jdwp=transport=dt_socket,address=30303,server=y,suspend=n -jar org.apache.sling.starter-11.jar