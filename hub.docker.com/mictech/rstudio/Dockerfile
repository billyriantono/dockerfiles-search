FROM centos:centos6
MAINTAINER Michal Tehnik <michal.tehnik@mictech.cz>

RUN yum update -y

#Install prerequesities
RUN yum install wget -y && \
yum install openssl098e -y

WORKDIR /root

#Download binaries
RUN wget ftp://ftp.is.co.za/mirror/fedora.redhat.com/epel/6/x86_64/R-core-3.0.2-1.el6.x86_64.rpm && \
wget ftp://ftp.is.co.za/mirror/fedora.redhat.com/epel/6/x86_64/R-core-devel-3.0.2-1.el6.x86_64.rpm && \
wget ftp://ftp.is.co.za/mirror/fedora.redhat.com/epel/6/x86_64/R-devel-3.0.2-1.el6.x86_64.rpm && \
wget ftp://ftp.is.co.za/mirror/fedora.redhat.com/epel/6/x86_64/R-java-devel-3.0.2-1.el6.x86_64.rpm && \
wget http://download2.rstudio.org/rstudio-server-0.98.1091-x86_64.rpm

#Install
RUN yum install R-core-3.0.2-1.el6.x86_64.rpm -y && \
yum install R-core-devel-3.0.2-1.el6.x86_64.rpm -y && \
yum install R-java-devel-3.0.2-1.el6.x86_64.rpm -y && \
yum install R-devel-3.0.2-1.el6.x86_64.rpm -y && \
yum install rstudio-server-0.98.1091-x86_64.rpm -y

#Port
EXPOSE 8888

ADD run.sh /root/run.sh
RUN chmod +x /root/run.sh

CMD ["/root/run.sh"]
