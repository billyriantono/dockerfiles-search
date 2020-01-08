# Arthur's CentOS 5 / Tomcat 6 base
FROM centos:5.11
MAINTAINER Art <arthur.crawford@webexpenses.com>

RUN yum install -y wget

# Install Sun JDK 1.5.0_22
RUN \
    cd /opt ;\
    wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" -O jdk-1_5_0_22-linux-amd64.bin http://download.oracle.com/otn-pub/java/jdk/1.5.0_22/jdk-1_5_0_22-linux-amd64.bin

RUN \
    cd /opt ;\
    echo yes|sh /opt/jdk-1_5_0_22-linux-amd64.bin ;\
    rm /opt/jdk-1_5_0_22-linux-amd64.bin

ENV JAVA_HOME /opt/jdk1.5.0_22
ENV PATH $JAVA_HOME/bin:$PATH

# Install apache ant 1.6.5
RUN \
    cd /opt ;\
    wget http://archive.apache.org/dist/ant/binaries/apache-ant-1.6.5-bin.tar.gz

RUN \
    cd /opt ;\
    tar xvfz apache-ant-1.6.5-bin.tar.gz ;\
    rm /opt/apache-ant-1.6.5-bin.tar.gz

ENV ANT_HOME /opt/apache-ant-1.6.5
ENV PATH $ANT_HOME/bin:$PATH

# Install tomcat 6.0.35
RUN \
    cd /opt ;\
    wget http://archive.apache.org/dist/tomcat/tomcat-6/v6.0.35/bin/apache-tomcat-6.0.35.tar.gz

RUN \
    cd /opt ;\
    tar xvfz  apache-tomcat-6.0.35.tar.gz ;\
    rm /opt/apache-tomcat-6.0.35.tar.gz

ENV CATALINA_HOME /opt/apache-tomcat-6.0.35
ENV PATH $CATALINA_HOME/bin:$PATH

