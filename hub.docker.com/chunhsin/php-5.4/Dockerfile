FROM centos:centos6
# Add EPEL Repo
RUN rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
# Add remi repo
RUN rpm -Uvg http://rpms.famillecollet.com/enterprise/remi-release-6.rpm

# Install basic packages
RUN yum -y install vim-enhanced bash-completion unzip glibc-common

# Install PHP
RUN yum -y --enablerepo=remi install httpd php php-pear php-gd php-mbstring php-mcrypt php-gettext php-xml php-common php-cli php-devel

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