FROM tomcat:8.5.37-jre8
MAINTAINER ravi@gmail.com
RUN apt-get update
COPY jenkins.war /usr/local/tomcat/webapps/
WORKDIR /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
