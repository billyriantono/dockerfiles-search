FROM centos:latest

MAINTAINER Yuriy Golik <eswees@pyhead.net>

LABEL Description="Linux + Apache + PHP. CentOS 7 based." \
      License="As is" \
      Usage="docker run -d -p [HOST PORT NUMBER]:80 eswees/rainloop" \
      Version="1.1"

EXPOSE  80

RUN yum install -y epel-release && yum update -y \
	&& yum install -y https://centos7.iuscommunity.org/ius-release.rpm \
	&& rpm --import /etc/pki/rpm-gpg/IUS-COMMUNITY-GPG-KEY \
	&& yum install -y \
		httpd \
		mod_php70u \
		php70u \
		php70u-cli \
		php70u-opcache \
		php70u-mbstring \
		php70u-json \
		php70u-dom \
		cyrus-sasl \
		cyrus-sasl-plain \
	&& yum clean all

COPY httpd.conf /etc/httpd/conf/httpd.conf

WORKDIR /var/www/html

ADD entry.sh /entry.sh
RUN chmod +x /entry.sh
ENTRYPOINT [ "/entry.sh" ]

#CMD /usr/sbin/apachectl -DFOREGROUND

VOLUME [ "/var/www/html" ]
