FROM centos:latest

MAINTAINER ztx9259 <ztx9259@hotmail.com>

# set PHP version
ENV PHP_VERSION 7.1.5

# install dependences
RUN set -x \
  && yum update -y \
  && yum install epel-release -y \
  && yum install -y wget git gcc gcc-c++ make automake autoconf perl file tar re2c libjpeg libpng libjpeg-devel libpng-devel libjpeg-turbo freetype freetype-devel \
        libcurl-devel libxml2-devel libjpeg-turbo-devel libXpm-devel libXpm libicu-devel libmcrypt libmcrypt-devel libxslt-devel libxslt openssl openssl-devel bzip2-devel \

  && mkdir ~/download \
  && cd ~/download \

# compile PHP
  && wget http://cn2.php.net/distributions/php-$PHP_VERSION.tar.gz \
  && tar -zxf php-$PHP_VERSION.tar.gz \
  && cd php-$PHP_VERSION \
  && groupadd -r nginx \
  && useradd -r -g nginx nginx \
  && ./configure \
       --prefix=/usr/local/php \
       --with-config-file-path=/usr/local/php/etc/ \
       --with-config-file-scan-dir=/usr/local/php/conf.d/ \
       --enable-fpm \
       --enable-cgi \
       --with-fpm-user=nginx  \
       --with-fpm-group=nginx \
       --disable-phpdbg \
       --enable-mbstring \
       --enable-calendar \
       --with-xsl \
       --with-openssl \
       --enable-soap \
       --enable-zip \
       --enable-shmop \
       --enable-sockets \
       --with-gd \
       --with-freetype-dir=/usr/include/freetype2/freetype \
       --with-jpeg-dir \
       --with-png-dir \
       --with-xpm-dir \
       --with-xmlrpc \
       --enable-pcntl \
       --enable-intl \
       --with-mcrypt \
       --enable-sysvsem \
       --enable-sysvshm \
       --enable-sysvmsg \
       --enable-opcache \
       --with-iconv \
       --with-bz2 \
       --with-curl \
       --enable-mysqlnd \
       --with-mysqli=mysqlnd \
       --with-pdo-mysql=mysqlnd \
       --with-zlib \
       --with-gettext \
  && make \
  && make install \

# add env
  && echo "export PATH=/usr/local/php/bin:/usr/local/php/sbin:$PATH" >> ~/.bashrc \
  && source ~/.bashrc \

# install composer
  && cd ~/download \
  && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php composer-setup.php --install-dir=/usr/local/sbin --filename=composer \
  && php -r "unlink('composer-setup.php');" \

  && rm -rf ~/download \
  && yum clean all

CMD ["/usr/local/php/sbin/php-fpm"]

EXPOSE 9000