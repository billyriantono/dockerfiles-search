FROM centos

# Maintainer
MAINTAINER "John Edisson Ortiz <john.ortiz@placetopay.com>"

# Mandatory packages
RUN yum -y update && yum -y install epel-release yum-utils

# Enable REMI REPO
RUN rpm -ivh http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    yum -y update && \
    yum-config-manager --enable remi-php73

# Install PHP and its extensions
RUN yum -y install \
    epel-release \
    git \
    unzip \
    php \
    php-common \
    php-mysql \
    php-mbstring \
    php-xml \
    php-simplexml \
    php-pdo \
    php-imap \
    php-soap \
    php-json \
    php-xmlrpc \
    php-gd \
    php-zip \
    php-intl

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
