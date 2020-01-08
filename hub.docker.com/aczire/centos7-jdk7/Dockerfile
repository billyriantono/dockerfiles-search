# JDK7 
FROM centos:centos7
MAINTAINER Jimson K James "mail.jimson@aczire.com"
ENV REFRESHED_AT 2014-12-01

# Install epel & CentOS Base repo
RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-2.noarch.rpm
RUN rm -f /etc/yum.repos.d/CentOS-Base.repo
# Hand coding the base repo file instead of ADD for breavity.
RUN echo "[base]" > /etc/yum.repos.d/CentOS-Base.repo
RUN echo "name=CentOS-\$releasever - Base" >> /etc/yum.repos.d/CentOS-Base.repo
RUN echo "mirrorlist=http://mirrorlist.centos.org/?release=\$releasever&arch=\$basearch&repo=os" >> /etc/yum.repos.d/CentOS-Base.repo
RUN echo "#baseurl=http://mirror.centos.org/centos/\$releasever/os/\$basearch/" >> /etc/yum.repos.d/CentOS-Base.repo
RUN echo "gpgcheck=0" >> /etc/yum.repos.d/CentOS-Base.repo

# Install wget
#RUN yum install -y --nogpgcheck wget

# Install Oracle JDK
RUN  curl -L --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; \
 oraclelicense=accept-securebackup-cookie" \
 "https://edelivery.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-linux-x64.rpm" -o jdk-7u72-linux-x64.rpm

#RUN wget http://192.168.56.1/jdk-7u71-linux-x64.rpm
RUN rpm -Uvh jdk-7u72-linux-x64.rpm
#RUN rpm -Uvh jdk-7u71-linux-x64.rpm
RUN rm jdk-7u72-linux-x64.rpm
#RUN rm jdk-7u71-linux-x64.rpm
RUN alternatives --install /usr/bin/java java /usr/java/latest/jre/bin/java 200000
RUN alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000
RUN alternatives --install /usr/bin/jar jar /usr/java/latest/bin/jar 200000
RUN java -version