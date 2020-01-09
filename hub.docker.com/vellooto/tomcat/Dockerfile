FROM centos:latest
LABEL mantainer="alexis.mura@gmail.com"

RUN yum update -y \
    && yum install -y wget

# Setup gosu for easier command execution
ENV GOSU_VERSION=1.10
RUN gpg --keyserver pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
    && curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64" \
    && curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64.asc" \
    && gpg --verify /usr/local/bin/gosu.asc \
    && rm /usr/local/bin/gosu.asc \
    && rm -r /root/.gnupg/ \
    && chmod +x /usr/local/bin/gosu

WORKDIR /opt

RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/server-jre-8u181-linux-x64.tar.gz" \
    && tar xvf server-jre-8u181-linux-x64.tar.gz \
    && ln -s jdk1.8.0_181 java \
    && rm server-jre-8u181-linux-x64.tar.gz

# Installation of Tomcat

RUN useradd -m -s /bin/bash tomcat \
    && wget "https://archive.apache.org/dist/tomcat/tomcat-7/v7.0.82/bin/apache-tomcat-7.0.82.tar.gz" \
    && tar xvf apache-tomcat-7.0.82.tar.gz \ 
    && ln -s apache-tomcat-7.0.82 tomcat \
    && rm apache-tomcat-7.0.82.tar.gz \
    && echo "export JAVA_HOME=/opt/java" >> /opt/tomcat/bin/setenv.sh \
    && echo "export CATALINA_HOME=/opt/tomcat" >> /opt/tomcat/bin/setenv.sh \
    && chmod +x /opt/tomcat/bin/setenv.sh \
    && chown -RL tomcat.tomcat tomcat

EXPOSE 8080

WORKDIR /root

ADD ["startup.sh", "."]

ENTRYPOINT ["./startup.sh"]
