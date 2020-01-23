#FROM  tomcat:8-jre8
FROM dbsync/secured-tomcat

MAINTAINER "Naveen-DBSync <naveen.p@mydbsync.com>"

RUN mkdir -p /usr/local/tomcat/c2c
COPY c2c /usr/local/tomcat/c2c
ADD ecw.xml /usr/local/tomcat/conf/Catalina/localhost/
