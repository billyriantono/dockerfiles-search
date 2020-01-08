FROM tomcat:8-jre8
MAINTAINER Docker Tester

COPY *.war /usr/local/tomcat/webapps/

EXPOSE 8080
CMD ["catalina.sh", "run"]
