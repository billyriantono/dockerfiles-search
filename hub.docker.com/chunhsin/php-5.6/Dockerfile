FROM centos:centos6

# EPEL
RUN rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
# Add repo
RUN rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm

RUN yum -y install php56w php56w-opcache php56w-common php56w-cli php56w-devel php56w-mbstring httpd php56w-mcrypt php56w-gd php56w-xml php56w-pdo

# short open tag
RUN sed -i "s/short_open_tag = .*/short_open_tag = On/g" /etc/php.ini
RUN chkconfig httpd on

# Using composer to manage PHP dependency
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# install npm (node js)
RUN yum -y install npm

#install bower
RUN npm install -g bower
RUN npm install -g gulp

# Install basic packages
RUN yum -y install vim-enhanced bash-completion unzip glibc-common

