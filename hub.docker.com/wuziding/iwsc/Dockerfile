FROM debian:jessie

MAINTAINER jasonszs <zhenshengshi@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

ENV NGINX_VERSION nginx-1.6
ENV APACHE_VERSION apache-2.4
ENV PHP_VERSION php-5.6
ENV MYSQL_VERSION mysql-5.5
ENV MONGODB_VERSION mongodb-3.2
ENV JDK_VERSION jdk-8u144
ENV MAVEN_VERSION maven-3.3.9
ENV TOMCAT_VERSION tomcat-8.0.45

ENV JAVA_HOME /opt/${JDK_VERSION}
ENV JRE_HOME $JAVA_HOME/jre
ENV CLASSPATH .:$JAVA_HOME/lib:$JRE_HOME/lib
ENV PATH $PATH:$JAVA_HOME/bin:$JRE_HOME/bin:/opt/${MAVEN_VERSION}/bin

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927 \
    && echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.2 main" | tee /etc/apt/sources.list.d/mongodb-org-3.2.list \
    && apt-get update \
    && apt-get install -y apt-utils wget apache2 mysql-server-5.5 php5 php5-mysql nginx mongodb-org \
    && apt-get -y dist-upgrade && apt-get autoremove && apt-get autoclean && rm -rf /var/lib/apt/lists/* \
    && wget --header "Cookie: oraclelicense=accept-securebackup-cookie" -O /tmp/${JDK_VERSION}.tar.gz http://download.oracle.com/otn-pub/java/jdk/8u144-b01/090f390dda5b47b9b721c7dfaa008135/jdk-8u144-linux-x64.tar.gz \
    && wget -O /tmp/${MAVEN_VERSION}.tar.gz https://archive.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz \
    && wget -O /tmp/${TOMCAT_VERSION}.tar.gz http://archive.apache.org/dist/tomcat/tomcat-8/v8.0.45/bin/apache-tomcat-8.0.45.tar.gz \
    && mkdir /opt/${JDK_VERSION} && tar -zxvf /tmp/${JDK_VERSION}.tar.gz -C /opt/${JDK_VERSION} --strip-components 1 && rm -rf /tmp/${JDK_VERSION}.tar.gz \
    && mkdir /opt/${MAVEN_VERSION} && tar -zxvf /tmp/${MAVEN_VERSION}.tar.gz -C /opt/${MAVEN_VERSION} --strip-components 1 && rm -rf /tmp/${MAVEN_VERSION}.tar.gz \
    && mkdir /opt/${TOMCAT_VERSION} && tar -zxvf /tmp/${TOMCAT_VERSION}.tar.gz -C /opt/${TOMCAT_VERSION} --strip-components 1 && rm -rf /tmp/${TOMCAT_VERSION}.tar.gz \
    && cp /etc/apache2/ports.conf /etc/apache2/ports.conf.bak \
    && chmod -R 777 /tmp

# apache2 listen 8088 port, because 80 is listened by nginx 
COPY files/apache2-ports.conf /etc/apache2/ports.conf
# add mongod to /etc/init.d/mongod, because it's not installed with mongodb-org.
COPY files/mongod-initd /etc/init.d/mongod

CMD /etc/init.d/mysql start \
    && /etc/init.d/mongod start \
    && /etc/init.d/nginx start \
    && /etc/init.d/apache2 start \
    && /opt/${TOMCAT_VERSION}/bin/startup.sh \
    && /bin/bash
 
VOLUME ["/var", \
        "/opt", \
        "/tmp"]
