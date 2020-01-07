FROM centos:6.6
MAINTAINER Nicolas FATREZ / DIREXI <nfatrez@direxi.com>

ENV APP_ENV development
ENV WWW /var/www/html
ENV PORT 80
ENV VHOST localhost.dev

RUN yum -y install wget httpd; yum clean all;
RUN yum -y install php php-mysql php-soap php-xml php-mbstring; yum clean all;
RUN cd /tmp; wget wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm; rpm -ivh epel-release-6-8.noarch.rpm; 
RUN yum -y install php-mcrypt; yum clean all;

RUN mkdir /etc/httpd/conf.d/vhosts
RUN grep -q -F 'Include "conf.d/vhosts/*.conf"' /etc/httpd/conf/httpd.conf  || echo 'Include "conf.d/vhosts/*.conf"' >> /etc/httpd/conf/httpd.conf

VOLUME /var/www/html
VOLUME /etc/httpd/conf.d/vhosts

# Copy script
COPY conf/template.conf /tmp
COPY run.sh /

# Entrypoint
CMD /bin/sh /run.sh
