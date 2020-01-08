# Use latest Fedora image as the base
FROM centos:6.6
MAINTAINER http://www.centos.org

LABEL Vendor="CentOS"
LABEL License=GPLv2
LABEL Version=6.6.Final


# Update base image
RUN yum -y update && yum clean all

# Install apache
RUN yum -y install httpd

# Install ssl module
RUN yum -y install mod_ssl

# Set the PHP_VERSION env variable
ENV PHP_VERSION 5.3.3-*

# Create the adminstall user and group
# RUN groupadd -r adminstall -g 433 && adminstall -u 431 -r -g adminstall -d /var/www -s /sbin/nologin -c adminstall_user adminstall

# Enable EPEL repository 
RUN cd /usr/src/ \
    && yum -y install wget \
	&& wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm \
	&& rpm -ivh epel-release-6-8.noarch.rpm \
	&& yum repolist \
	&& yum -y update

# Install suhosin
RUN yum -y --noplugins install php-devel

RUN wget ftp://ftp.is.co.za/mirror/fedora.redhat.com/epel/6/x86_64/php-suhosin-0.9.29-2.el6.x86_64.rpm \
    && rpm -ivh php-suhosin-0.9.29-2.el6.x86_64.rpm \
	&& yum repolist \
	&& yum -y update



# Install php
RUN yum -y install php-$PHP_VERSION
RUN yum -y install php.x86_64 \
 php-cli.x86_64 \
 php-common.x86_64 \
 php-gd.x86_64 \
 php-ldap.x86_64 \
 php-mbstring.x86_64 \
 php-mcrypt.x86_64 \
 php-mysql.x86_64 \
 php-pdo.x86_64 \
 php-pear.noarch \
 php-pear-Auth-SASL.noarch \
 php-pear-DB.noarch \
 php-pear-HTTP-Request.noarch \
 php-pear-Log.noarch \
 php-pear-MDB2.noarch \
 php-pear-Mail.noarch \
 php-pear-Mail-Mime.noarch \
 php-pear-Net-DIME.noarch \
 php-pear-Net-SMTP.noarch \
 php-pear-Net-Socket.noarch \
 php-pear-Net-URL.noarch \
 php-pear-Numbers-Words.noarch \
 php-pear-OLE.noarch \
 php-pear-PHP-Compat.noarch \
 php-pear-SOAP.noarch \
 php-pear-Spreadsheet-Excel-Writer.noarch \
 php-pgsql.x86_64 \
 php-soap.x86_64 \
 php-suhosin.x86_64 \
 php-xml.x86_64 \
 php-xmlrpc.x86_64 \
 php-suhosin

# Edit file php.ini
#RUN sed -i "s/short_open_tag = Off/short_open_tag = On/g" /etc/php.ini
#RUN sed -i "s/display_errors = Off/display_errors = On/g" /etc/php.ini
#RUN echo include_path=".:/usr/share/pear:/usr/share/php:/var/www/html" >> /etc/php.ini 
#RUN echo date.timezone = America/Bogota >> /etc/php.ini 

# Add files
RUN mkdir /etc/perseo
RUN mkdir /var/log/portales
RUN chmod 777 /var/log/portales
RUN chmod 777 /var/www/html
COPY pear /usr/share/pear
COPY php /usr/share/php
COPY etc /etc

#Config date
RUN yes | cp /usr/share/zoneinfo/America/Bogota /etc/localtime

# Expose the ports we're interested in
EXPOSE 80
EXPOSE 443

# Run everything below as the wildfly user
# USER adminstall

# Set the default command to run on boot
ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["-D", "FOREGROUND"]