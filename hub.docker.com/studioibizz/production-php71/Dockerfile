FROM centos:centos7
RUN yum update -y && yum install httpd httpd-tools -y

RUN yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y
RUN yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y

RUN yum install yum-utils -y
RUN yum install mc -y

# Changed the current timezone to Europe/Amsterdam
RUN rm -f /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime

RUN yum-config-manager --enable remi-php71 -y

RUN yum -y install gcc

RUN yum -y install cronie

# install php7
# breaking it down to see where dockerhub dies.
RUN \
	yum -y install \
		php php-common \
		php-devel \
		php-mbstring \
		php-mcrypt \
		php-pear \
		php-xml \
		php-mysqlnd \
		php-pdo \
		php-opcache --nogpgcheck \
		php-bcmath \
		php-soap \
		php-gd

# php-fpm
RUN yum -y install php-fpm

# SSL
RUN yum -y install mod_ssl \
                   openssl

# Zip
RUN yum -y install zip \
                   unzip \
                   php-zip

# Install ImageMagick
RUN yum -y install ImageMagick \
                   ImageMagick-devel

RUN pecl install imagick
COPY ini/60-imagemagick.ini /etc/php.d/60-imagemagick.ini

# Copied custom configuration for alias
COPY conf/vhost.conf /etc/httpd/conf.d/wingzz-vhost.conf

# Install the latest version of CVS
RUN yum -y install wget
RUN wget https://www.mercurial-scm.org/release/centos7/mercurial-4.9-1.x86_64.rpm
RUN rpm -Uvh mercurial-4.9-1.x86_64.rpm

RUN yum -y install \
        mercurial \
        git

# Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN composer global require hirak/prestissimo

EXPOSE  80 443

# Copied script file to run every time
COPY scripts/start.sh /root/scripts/start.sh
RUN ["chmod", "+x", "/root/scripts/start.sh"]

CMD ["/root/scripts/start.sh"]
