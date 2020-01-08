# Copyright (c) 2016 julien,
# Contributors:
# Julien Cosso

FROM centos:7
EXPOSE 4403 8080 8000 22


RUN yum update -y && \
    yum -y install sudo openssh-server procps wget unzip mc git curl subversion nmap && \
    mkdir /var/run/sshd && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd -u 1000 -G users,wheel -d /home/user --shell /bin/bash -m user && \
    echo -e "codenvy2016\ncodenvy2016" | passwd user && \
    sed -i 's/requiretty/!requiretty/g' /etc/sudoers && \
        chmod 777 /opt

# Install Java 6 SDK




# Install Java SDK
WORKDIR /opt
# Install Oracle Java 6 SDK
ENV JAVA_VERSION=jdk1.6.0_45
ENV JAVA_HOME=/opt/java/${JAVA_VERSION}
ENV JDK_FILE=jdk-6u45-linux-x64.bin
# Install Java SDK
RUN wget -q --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" -O "/opt/${JDK_FILE}" "http://download.oracle.com/otn-pub/java/jdk/6u45-b06/${JDK_FILE}" && \
    chmod +x /opt/${JDK_FILE} && \
        /opt/${JDK_FILE} && \
        rm -rf /opt/${JDK_FILE} && rm -rf /var/log/*

ENV JAVA_VERSION=8u45
ENV JAVA_VERSION_PREFIX=1.8.0_45 



RUN  wget \
  --no-cookies \
  --no-check-certificate \
  --header "Cookie: oraclelicense=accept-securebackup-cookie" \
  -qO- \
  "http://download.oracle.com/otn-pub/java/jdk/$JAVA_VERSION-b14/jdk-$JAVA_VERSION-linux-x64.tar.gz" | tar -zx -C /opt/ 


ENV JAVA_HOME=/opt/jdk$JAVA_VERSION_PREFIX 

USER user

LABEL che:server:8080:ref=tomcat che:server:8080:protocol=http che:server:8000:ref=tomcat-debug che:server:8000:protocol=http

ENV MAVEN_VERSION=3.3.9 \
    TOMCAT_HOME=/home/user/tomcat



ENV M2_HOME=/home/user/apache-maven-$MAVEN_VERSION

ENV PATH=$JAVA_HOME/bin:$M2_HOME/bin:$PATH

RUN mkdir /home/user/tomcat && mkdir /home/user/apache-maven-$MAVEN_VERSION && \
  wget -qO- "http://apache.ip-connect.vn.ua/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz" | tar -zx --strip-components=1 -C /home/user/apache-maven-$MAVEN_VERSION/

ENV TERM xterm

RUN wget -qO- "http://archive.apache.org/dist/tomcat/tomcat-6/v6.0.45/bin/apache-tomcat-6.0.45.tar.gz" | tar -zx --strip-components=1 -C /home/user/tomcat && \
    rm -rf /home/user/tomcat/webapps/*
USER root
RUN  echo -e "JAVA_HOME=$JAVA_HOME\nM2_HOME=/home/user/apache-maven-$MAVEN_VERSION\nTOMCAT_HOME=/home/user/tomcat\nPATH=$JAVA_HOME/bin:$M2_HOME/bin:$PATH" >> /etc/environment
USER user
ENV LANG=fr_FR.UTF-8

WORKDIR /projects

CMD sudo /usr/bin/ssh-keygen -A && \
     sudo /usr/sbin/sshd -D && \
    tail -f /dev/null
