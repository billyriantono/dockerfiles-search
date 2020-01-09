# tcloud/usergrid
# VERSION        0.1

FROM tcloud/tomcat:8
MAINTAINER tcloud

USER root

ENV USERGRID_HOME /usr/local/tomcat/current
ENV PATH ${USERGRID_HOME}/bin:$PATH

WORKDIR ${USERGRID_HOME}

VOLUME ["/usr/local/tomcat/current/conf","/usr/local/tomcat/current/logs","/usr/local/tomcat/current/webapps", "/data","/log"]

EXPOSE 8080

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
ENTRYPOINT ["sh", "-c"]

CMD $CATALINA_HOME/bin/catalina.sh run