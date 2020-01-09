FROM centos:centos7.7.1908
MAINTAINER "kongfanhong@docker.com"
# centos:centos7.7.1908, jre-8u211,tomcat-8.5.41

### timezone
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' > /etc/timezone

ENV LANG="en_US.UTF-8" \
    LANGUAGE="en_US:en" \
    LC_ALL="en_US.UTF-8"

ENV JAVA_VERSION="1.8.0_211"

### install jre
ADD jre-8u211-linux-x64.tar.gz /usr/local/

ENV JAVA_HOME="/usr/local/jre${JAVA_VERSION}"
ENV PATH="$JAVA_HOME/bin:$PATH"

ENV JAVA_OPTS="-Dspring.profiles.active=default"


ENV TOMCAT_VERSION="apache-tomcat-8.5.50"
### install tomcat
ADD "$TOMCAT_VERSION.tar.gz" /usr/local/

ENV CATALINA_HOME /usr/local/$TOMCAT_VERSION
ENV PATH $CATALINA_HOME/bin:$PATH
WORKDIR $CATALINA_HOME

EXPOSE 8080

### install myweb
#ADD myweb.war /usr/local/$TOMCAT_VERSION/webapps/

### start tomcat
CMD ["catalina.sh", "run"]
