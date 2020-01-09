FROM tomcat:8-jre8
MAINTAINER KAMAL CHAUHAN
RUN rm -rf /usr/local/tomcat/webapps/*
COPY gameoflife.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]
