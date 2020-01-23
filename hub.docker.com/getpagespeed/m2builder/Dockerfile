FROM centos:7

RUN yum -y install epel-release
RUN yum -y install -y openssh-clients git rsync
RUN yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
RUN yum-config-manager --enable remi-php71
RUN yum -y install composer \
  php-cli \
  php-fpm \
  php-common \
  php-json \
  php-pecl-zip \
  php-opcache \
  php-mysqlnd \
  php-mcrypt \
  php-soap \
  php-gd \
  php-pecl-imagick \
  php-mbstring \
  php-pecl-apcu \
  php-xml \
  php-tidy \
  php-pecl-memcached \
  php-ioncube-loader \
  php-bcmath \
  php-intl 
