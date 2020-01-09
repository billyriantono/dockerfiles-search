# imagem docker
FROM tomcat:7.0

# autor
MAINTAINER Erik Andreazi <erik@treetools.com.br>

#ENV JAVA_OPTS="-XX:PermSize=1024m -XX:MaxPermSize=512m"
# tomcat
#ENV TOMCAT_VERSION_MAJOR 7
#ENV TOMCAT_VERSION_FULL 7.0.96
#ENV CATALINA_HOME /opt/tomcat

# Download and install Java
#RUN apk --update add --update curl &&\
#	curl -LO http://www1.treetools.com.br/Suporte/Download/jdk-8u221-linux-x64.tar.gz &&\
#	tar -xvzf jdk-8u221-linux-x64.tar.gz -C /opt &&\
#RUN mkdir -p /usr/local/tomcat/conf && \
#    mkdir -p /usr/local/tomcat/webapps &&\
#    mkdir -p /usr/local
#    ln -s /opt/jdk1.8.0_221 /opt/jdk
	
# Download and install Java
#	RUN apk --update add --update curl &&\
#	curl -LO http://mirror.nbtelecom.com.br/apache/tomcat/tomcat-${TOMCAT_VERSION_MAJOR}/v${TOMCAT_VERSION_FULL}/bin/apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz &&\
#	tar -xvzf apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz -C /opt &&\
#	rm -f apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz &&\
#	mkdir /opt/tomcat &&\
#	ln -s /opt/apache-tomcat-${TOMCAT_VERSION_FULL} /opt/tomcat &&\
#	rm -rf /opt/tomcat/webapps/examples /opt/tomcat/webapps/docs &&\
RUN mkdir -p /SB3/LIC/

# usuarios do tomcat
COPY license.LIC /SB3/LIC/
COPY tomcat-users.xml context.xml /usr/local/tomcat/conf/
COPY jar/*.jar /usr/local/tomcat/lib/
