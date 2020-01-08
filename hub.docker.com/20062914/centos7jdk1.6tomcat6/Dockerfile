FROM 20062914/centos

MAINTAINER lint <lint@heerit.com>



RUN	cd /opt/heer \
		&& wget "http://mirror.bit.edu.cn/apache/tomcat/tomcat-6/v6.0.53/bin/apache-tomcat-6.0.53.tar.gz" \
		&& tar -xzvf ./apache-tomcat-6.0.53.tar.gz \
		&& mv apache-tomcat-6.0.53 apache-tomcat-6.0.45 \
		&& rm ./apache-tomcat-6.0.53.tar.gz \
		&& rm -rf ./apache-tomcat-6.0.45/webapps/* \
		&& mkdir ./server
ENV CATALINA_HOME /opt/heer/apache-tomcat-6.0.45
