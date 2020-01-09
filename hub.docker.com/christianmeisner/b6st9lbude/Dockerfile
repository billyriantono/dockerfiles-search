FROM tomcat:9-jre8  
MAINTAINER christianmeisner
WORKDIR /app

EXPOSE 8009 8080

RUN apt-get update && apt-get install -y --no-install-recommends iputils-ping less nano

#RUN echo "export JAVA_OPTS=\"-Dapp.env=staging\"" > /usr/local/tomcat/bin/setenv.sh  
COPY Eurostudent-Albania.war /usr/local/tomcat/webapps/Eurostudent-Albania.war
COPY tomcat-users.xml /usr/local/tomcat/conf/tomcat-users.xml
COPY context.xml /usr/local/tomcat/webapps/manager/META-INF/context.xml
COPY server.xml /usr/local/tomcat/conf/server.xml
COPY catalina.sh /usr/local/tomcat/bin/catalina.sh

CMD ["catalina.sh", "run"]  
