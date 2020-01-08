FROM centos:5.11

MAINTAINER Chrometaro <chrometaro@gmail.com>

COPY ./yum.repos.d/ /etc/yum.repos.d/

ADD https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL /etc/pki/rpm-gpg/RPM-GPG-KEY-PGDG

RUN yum update -y \
 && yum install -y \
    php \
    php-devel \
    php-gd \
    php-mbstring \
    php-mysql \
    php-odbc \
    php-pdo \
    php-pear \
    php-pgsql \
    php-xml \
 && yum clean all \
 && pear install \
    Mail-1.2.0 \
    Mail_Mime-1.8.1 \
    Archive_Zip-0.1.1 \
    DB-1.7.13 \
    OLE-1.0.0RC1 \
    HTTP_Request

COPY httpd-foreground /usr/local/bin/

EXPOSE 22 80 443
CMD ["httpd-foreground"]
