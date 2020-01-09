FROM centos:centos6

MAINTAINER Andres Sanchez Garcia <asg1612@gmail.com>

#ADD CentOS-Base.repo etc/yum.repos.d/
RUN yum install -y wget
RUN wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
RUN rpm -Uvh rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
RUN wget http://dl.fedoraproject.org/pub/epel/6Server/i386/epel-release-6-8.noarch.rpm
RUN rpm -Uvh epel-release-6-8.noarch.rpm

RUN yum -y install amavisd-new clamav clamav-devel clamd spamassassin postfix syslog-ng syslog-ng-libdbi
ADD clamd.conf /etc/
ADD amavisd.conf /etc/amavisd/
ADD master.cf /etc/postfix/
RUN echo "content_filter=amavisfeed:[127.0.0.1]:10024" >> /etc/postfix/main.cf
ADD syslog-ng.conf /etc/syslog-ng/


#CMD service httpd start ; bash

EXPOSE 25
EXPOSE 80
cmd ["sh", "-c", "service syslog-ng start ; service postfix start ; tail -F /var/log/maillog"] 
