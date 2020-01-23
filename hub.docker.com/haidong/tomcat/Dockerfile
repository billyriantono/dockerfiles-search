FROM haidong/java
MAINTAINER haidong <383623085@qq.com>

ARG TOMCAT_VERSION=8.5.16
ENV TOMCAT_HOME=/opt/tomcat

# Download and extract tomcat to opt folder
RUN curl -L http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz \    
    | tar -zx -C /opt \
    && ln -s /opt/apache-tomcat-${TOMCAT_VERSION} ${TOMCAT_HOME}
	
EXPOSE 8080
CMD ${TOMCAT_HOME}/bin/catalina.sh run