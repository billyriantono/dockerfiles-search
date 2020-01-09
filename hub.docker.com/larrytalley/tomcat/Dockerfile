FROM tomcat:9.0
MAINTAINER Larry Talley (larryt@acm.org)

USER root
    
RUN adduser --system --group --home $CATALINA_HOME --no-create-home tomcat && \
    chown -R tomcat:tomcat $CATALINA_HOME && \
    chown -h tomcat:tomcat $CATALINA_HOME
    
USER tomcat
