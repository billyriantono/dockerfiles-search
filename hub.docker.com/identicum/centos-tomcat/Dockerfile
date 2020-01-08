FROM identicum/centos-java:latest
MAINTAINER Gustavo J Gallardo <ggallard@identicum.com>

ENV CATALINA_HOME /usr/local/tomcat
ENV TOMCAT_VERSION 9.0.29

ENV PATH $CATALINA_HOME/bin:$PATH
RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME

RUN yum -y install wget

RUN useradd -m -U -d $CATALINA_HOME -s /bin/false tomcat && \
    wget https://www-eu.apache.org/dist/tomcat/tomcat-9/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz -O /tmp/tomcat.tgz && \
    tar -xvzf /tmp/tomcat.tgz --directory /tmp/ && \
    rm -f /tmp/tomcat.tgz && \
    mv /tmp/apache-tomcat-$TOMCAT_VERSION/* . && \
    chown -R tomcat: ./*

COPY context.xml ./webapps/manager/META-INF/
COPY tomcat-users.xml ./conf/

RUN rm -rf ./webapps/docs/ && \
    rm -rf ./webapps/examples/ && \
    rm -rf ./webapps/ROOT/*

RUN echo "<%= \"https://github.com/Identicum/docker-base-images/tree/master/centos-tomcat\" %>" > webapps/ROOT/index.jsp

EXPOSE 8080
CMD ["catalina.sh", "run"]
