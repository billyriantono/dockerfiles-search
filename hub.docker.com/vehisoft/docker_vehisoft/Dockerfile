FROM tomcat:7.0-jre7
RUN ["apt-get", "update"]
COPY spring-mvc.war /usr/local/tomcat/webapps/
COPY mail-1.4.7.jar /usr/local/tomcat/lib
EXPOSE 8080
CMD ["catalina.sh", "run"]
