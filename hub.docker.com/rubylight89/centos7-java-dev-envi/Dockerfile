#Author : yun
#Created date: 20170607

# implement base image centos:centos7
FROM centos:centos7
MAINTAINER duong phan

#RUN useradd interdev 
#RUN su interdev

# install sudo 
RUN yum -y install sudo

# install 
RUN yum -y install systemd

# install wget
RUN yum -y install wget

# install java
RUN yum -y install java-1.7.0-openjdk-devel
ENV JAVA_HOME=/usr/lib/jvm/java-1.7.0-openjdk-1.7.0.141-2.6.10.1.el7_3.x86_64
#type -p javac|xargs readlink -f|xargs dirname|xargs dirname
ENV PATH $PATH:$JAVA_HOME/bin
ENV JAVA_JRE=$JAVA_HOME/jre
ENV CLASS_PATH=$JAVA_HOME/bin

# install apache
RUN yum -y install httpd
# backup httpd.conf file
RUN cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.bu
# add configuration file
ADD resource/httpd.conf /etc/httpd/conf/httpd.conf

# install nignx 
RUN yum -y install epel-release
RUN yum -y install nginx

# install tomcat 7
RUN yum -y install tomcat
RUN yum install -y tomcat-webapps tomcat-admin-webapps

# install maven
RUN yum -y install maven

# install git
RUN yum -y install git

# Setting git ssh-key
RUN mkdir /root/.ssh/
ADD resource/id_rsa /root/.ssh/id_rsa
RUN chmod 700 /root/.ssh/id_rsa

# Create known_hosts
RUN touch /root/.ssh/known_hosts

# Add bitbuckets key (Add entry for host)
RUN ssh-keyscan bitbucket.org >> /root/.ssh/known_hosts

# Pull source 
RUN git clone git@bitbucket.org:rubylight89/sample.git workspace/source





