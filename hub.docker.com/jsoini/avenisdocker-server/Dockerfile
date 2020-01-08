FROM centos:centos7.5.1804
MAINTAINER Avenis Oy
LABEL apache.version=2.4 \
      php.version=7.2

#ARG sshuser=juujuu
#ARG sshuserpwd=joojoo
#ARG domain=avenis.local
#ENV SSHUSER=$sshuser
#ENV SSHUSERPWD=$sshuserpwd
#ENV DOMAIN=$domain

RUN yum clean all

RUN yum -y update && \
    yum -y install httpd \
    ImageMagick \
    java-1.7.0-openjdk \
    libpng \
    libjpeg \
    openssl \
    vim \
    curl \
    icu \
    libX11 \
    libXext \
    libXrender \
    xorg-x11-fonts-Type1 \
    xorg-x11-fonts-75dpi \
    python2-certbot-apache \
    sendmail \
    rsyslog \
    epel-release \
    yum-utils \
    cronie \
    wget

RUN yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    yum-config-manager --enable remi-php72

RUN yum -y install php \
    php-mysqlnd \ 
    php-pecl-zip \ 
    php-mbstring \
    php-intl \
    php-pecl-imagick \
    php-xmlrpc

RUN cd /tmp && \
    wget https://downloads.wkhtmltopdf.org/0.12/0.12.2.1/wkhtmltox-0.12.2.1_linux-centos7-amd64.rpm && \
    rpm -Uvh wkhtmltox-0.12.2.1_linux-centos7-amd64.rpm && \
    rm wkhtmltox-0.12.2.1_linux-centos7-amd64.rpm

COPY ./httpd.conf /etc/httpd/conf/httpd.conf

EXPOSE 443
EXPOSE 80
EXPOSE 82