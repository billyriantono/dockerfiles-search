FROM wxinqwxq/centos7-java8:jre8

ENV TOMCAT_MAJOR_VERSION 7
ENV TOMCAT_MINOR_VERSION 7.0.34
ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH

# INSTALL TOMCAT
RUN  wget -q https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz && \
     wget -qO- https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz.md5 | md5sum -c - && \
     tar zxf apache-tomcat-*.tar.gz && \
     rm apache-tomcat-*.tar.gz && \
     mv apache-tomcat* ${CATALINA_HOME} && \
     rm -rf ${CATALINA_HOME}/webapps/examples && \
     rm -rf ${CATALINA_HOME}/webapps/docs && \
     rm -rf ${CATALINA_HOME}/webapps/ROOT && \
     rm -rf ${CATALINA_HOME}/webapps/host-manager && \
     rm -rf ${CATALINA_HOME}/bin/*.bat

RUN chmod +x ${CATALINA_HOME}/bin/*.sh

# add volume for webapps folder
#VOLUME ${CATALINA_HOME}/webapps

RUN groupadd -r tomcat -g 433 && \
    useradd -u 431 -r -g tomcat -d ${CATALINA_HOME} -s /sbin/nologin -c "Docker image user" tomcat && \
    chown -R tomcat:tomcat ${CATALINA_HOME}

USER tomcat

EXPOSE 8080 8009

CMD ["catalina.sh", "run"]
