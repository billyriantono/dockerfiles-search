# =============================================================================
# Dockerfile automated Docker Hub build - Base image for other ones
#
# CentOS-6 
# EPEL Repo 
# Supervisor
# Apache 2.2
# PHP 5.6
# MOD_FCGID 2.3
# Memcached
# =============================================================================

# =============================================================================
# OPCACHE modified options in php.ini for developing
# =============================================================================
# ;opcache.revalidate_freq=60
# opcache.revalidate_freq=0
# ;opcache.validate_timestamps=0
# opcache.validate_timestamps=1
# =============================================================================

FROM centos:centos6

MAINTAINER Supermasita <supermasita@supermasita.com>

ENV UPDATED "2016-12-05"

## Import the Centos-6 RPM GPG key to prevent warnings and Add EPEL Repository
RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6 \
    && rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-6 \
    && rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm 

## USERS
RUN useradd www-data 

### YUM
RUN yum -y install \
    python-pip \
    openssh-clients \
    curl \
    cronie \
    rsyslog \
    ntpdate \
    gcc \
    wget \
    supervisor \
    tar \
    bzip \
    autoconf \
    libtool \
    automake \
    zlib-devel \
    openssl-devel \
    git \
    mysql \
    memcached \
    libxml2-devel \
    libcurl-devel \
    bzip2-devel \
    libjpeg-turbo-devel \
    libpng-devel \
    freetype-devel \
    libmcrypt-devel 
 
RUN rm -rf /var/cache/yum/* && yum clean all

## CRON
RUN echo -e "*/15 * * * * /usr/sbin/ntpdate ar.pool.ntp.org > /tmp/ntpdate.cron.out 2>&1" > /var/spool/cron/root


## UTC Timezone & Networking
RUN ln -sf /usr/share/zoneinfo/America/Argentina/Buenos_Aires /etc/localtime \
    && echo -e "NETWORKING=yes\nHOSTNAME=centos6" > /etc/sysconfig/network

## APACHE
RUN wget http://apache.dattatec.com/httpd/httpd-2.2.31.tar.gz -O /usr/local/src/httpd-2.2.31.tar.gz
RUN cd /usr/local/src/ && tar xvf httpd-2.2.31.tar.gz
RUN cd /usr/local/src/httpd-2.2.31 && ./configure --enable-module=so --prefix=/usr/local/apache-2.2.31 --with-mpm=worker --enable-module=expires --enable-module=headers --enable-rewrite --enable-vhost_alias --enable-headers --enable-expires --enable-info --enable-mem-cache --enable-disk-cache --enable-cache --enable-file-cache --enable-deflate --enable-ssl
RUN cd /usr/local/src/httpd-2.2.31 && make && make install
RUN ln -s /usr/local/apache-2.2.31 /usr/local/apache2

## MOD_FCGID
RUN wget http://apache.claz.org//httpd/mod_fcgid/mod_fcgid-2.3.9.tar.gz -O /usr/local/src/mod_fcgid-2.3.9.tar.gz
RUN cd /usr/local/src/ && tar xvf mod_fcgid-2.3.9.tar.gz
RUN cd /usr/local/src/mod_fcgid-2.3.9 && APXS=/usr/local/apache2/bin/apxs ./configure.apxs && make && make install

## PHP
RUN wget http://php.net/get/php-5.4.32.tar.gz/from/this/mirror  -O /usr/local/src/php-5.4.32.tar.gz 
RUN cd /usr/local/src/ && tar -zxvf php-5.4.32.tar.gz
RUN cd /usr/local/src/php-5.4.32 && ./configure --enable-mbstring --with-mysql --with-mysqli --with-zlib --with-png-dir=/usr --with-jpeg-dir=/usr --with-freetype-dir=/usr --with-curl --with-gettext --with-pdo-mysql --with-pdo-sqlite --with-bz2 --prefix=/usr/local/php-5.4.32/ --with-libdir=lib64 --with-gd --with-libdir=lib64 --enable-cgi --enable-sockets --with-mcrypt --enable-soap --with-openssl --enable-opcache 
RUN cd /usr/local/src/php-5.4.32 && make && make install 
RUN ln -s /usr/local/php-5.4.32 /usr/local/php
RUN ln -s /usr/local/php/bin/php /usr/bin/php
RUN ln -s /usr/local/php/bin/pear /usr/bin/pear
RUN ln -s /usr/local/php/bin/php-pear /usr/bin/php-pear

## CLEAN UP
RUN rm -fr /usr/local/src/*

## PECL MEMCACHE
RUN yes | /usr/local/php/bin/pecl install memcache-3.0.8

## PECL ZIP
RUN /usr/local/php/bin/pecl install zip-1.12.4

## PECL APC
RUN yes no | /usr/local/php/bin/pecl install apc

## PHP INI
ADD php.ini /usr/local/php/lib/

## HTTPD CONF
ADD httpd.conf /usr/local/apache2/conf/
RUN mkdir /usr/local/apache2/conf/virtuales/
ADD httpd-fastcgid.conf /usr/local/apache2/conf/extra/
RUN mkdir /var/log/apache2/
ADD 000-default.conf /usr/local/apache2/conf/virtuales/
RUN mkdir /data && chown www-data. /data
#RUN mkdir /var/www && chown -R www-data. /var/www
RUN ln -s /data /var/www

## SUPERVISOR CONF
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

## PORTS
EXPOSE 22 80 8080 443 9187 8088 6084 11211 11311


## RUN, FORREST! RUN!
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
