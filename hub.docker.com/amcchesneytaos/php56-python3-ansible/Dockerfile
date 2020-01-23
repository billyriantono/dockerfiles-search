From centos:7

# Install deltarpm for faster downloads
RUN yum install deltarpm -y

# Install PHP
RUN yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y \
    && yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y \
    && yum install yum-utils -y \
    && yum-config-manager --enable remi-php56 \
    && yum install php -y


# Install newer git to allow for depth options
RUN yum install http://opensource.wandisco.com/centos/7/git/x86_64/wandisco-git-release-7-2.noarch.rpm -y \
    && yum update -y \
    && yum install git -y


# Install Python 
RUN yum install -y https://centos7.iuscommunity.org/ius-release.rpm \
    && yum update -y \
    && yum install -y python36 python36-libs python36-devel python36-pip

RUN yum install -y git zip unzip vim

RUN pip3 install ansible


# Shortcut to reduce build times
RUN yum install -y \
    git \
    unzip \
    zip \
    vim \
    python3 \
    python3-pip \
    php \
    php-xml \
    php-mbstring \
    php-intl \
    php-mysql

RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp

ENV LC_ALL=en_US.utf-8
ENV LANG=en_US.utf-8


#Install GSUtils
RUN curl https://sdk.cloud.google.com | bash

ENV PATH "$PATH:/root/google-cloud-sdk/bin"