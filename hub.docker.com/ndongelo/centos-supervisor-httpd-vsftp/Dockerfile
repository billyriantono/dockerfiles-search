FROM centos

MAINTAINER Aurelio C Ndong Elo aureliondongelo@gmail.com

RUN \

yum update -y && \

yum install -y epel-release && \

yum install -y iproute python-setuptools hostname inotify-tools yum-utils which lynx && \
	 
yum clean all

RUN easy_install supervisor

RUN yum -y install httpd

RUN systemctl enable httpd

RUN yum -y install vsftpd

ADD config /

RUN systemctl enable vsftpd

	ENV USER=aurelio
	ENV PASSWORD=admin
	EXPOSE 9001 80 21 20
RUN \
	sed -ri "s/aurelio/${USER}/g" /etc/supervisord.conf && \
	sed -ri "s/admin/${PASSWORD}/g" /etc/supervisord.conf  
	ENTRYPOINT ["/config/bootstrap.sh"]
