FROM tomcat:latest
MAINTAINER Flavio Magacho 'flavio@magacho.com'

RUN sed -i '37i\\<user username="magacho" password="magacho" roles="standard,manager-script,manager-gui,manager-status,manager-jmx"/>\ ' /usr/local/tomcat/conf/tomcat-users.xml

EXPOSE 8080
CMD ["catalina.sh", "run"]
