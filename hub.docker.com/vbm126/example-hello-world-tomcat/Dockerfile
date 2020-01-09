FROM tomcat
ADD https://tomcat.apache.org/tomcat-9.0-doc/appdev/sample/sample.war .
RUN ls -ltr
RUN cp sample.war /usr/local/tomcat/webapps/
EXPOSE 8080
