FROM tomcat:8.5.16-jre8

RUN rm -rf $CATALINA_HOME/webapps/*

ADD eno-ws.war $CATALINA_HOME/webapps/eno-ws.war
ADD eno.properties $CATALINA_HOME/webapps/eno.properties

CMD ["catalina.sh", "run"]
