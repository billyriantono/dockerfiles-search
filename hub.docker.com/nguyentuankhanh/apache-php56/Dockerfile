FROM centos:centos6

MAINTAINER KhanhNT nguyen.tuankhanh@rivercrane.vn

#Install repository
RUN yum -y localinstall http://rpms.famillecollet.com/enterprise/remi-release-6.rpm

#Install Apache
RUN yum install -y httpd

#Intall PHP 5.6
RUN yum install -y --enablerepo=remi,remi-php56 php php-mysql php-pear php-gd php-mcrypt php-ldap php-xcache php-devel php-mbstring php-pdo php-pecl-xdebug php-pecl-memcache php-xml php-process libcurl-devel libxml2-devel mod_ssl pcre-devel libtool

#Install Composer
RUN curl  -k -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

#Clean yum cache
RUN yum clean -y all

#Add volume
VOLUME ["/var/www/html"]

#Open port 80,443
EXPOSE 80 443

#Add config here