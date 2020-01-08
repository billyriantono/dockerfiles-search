FROM 20062914/centos7jdk8

MAINTAINER lint <lint@heerit.com>



RUN	cd /opt/heer \
		&& wget "http://archive.apache.org/dist/tomcat/tomcat-7/v7.0.78/bin/apache-tomcat-7.0.78.tar.gz" \
		&& tar -xzvf ./apache-tomcat-7.0.78.tar.gz \
		&& mv ./apache-tomcat-7.0.78 ./tomcat \
		&& rm ./apache-tomcat-7.0.78.tar.gz \
		&& rm -rf ./tomcat/webapps/* \
		&& mkdir ./server
ENV CATALINA_HOME /opt/heer/tomcat
