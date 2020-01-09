# Image for WE WEB
FROM amazonlinux:1
LABEL maintainer="nguyentruonghuy93@gmail.com"
EXPOSE 9007 80 443
WORKDIR /root

# Install Dependiences of Nginx and Php7.1.x 
RUN yum -y install wget \ 
  epel-release \ 
  git \
  nano \
  autoconf \
  dos2unix  \ 
  nginx \
  GeoIP \
  GeoIP-devel \
  GeoIP-data \
  curl-devel \
  curl \
  libjpeg-devel \
  libpng-devel \
  freetype-devel \
  gd \
  gd-devel \
  rpm \
  rpm-devel \
  libxml2-devel \
  libxslt-devel \
  gcc \
  gcc-c++ \
  openssl-devel \
  libicu-devel \
  mysql-devel \
  libmcrypt-devel \
  libmhash-devel \
  libXpm \
  libxml2 \
  libXpm-devel \
  php-xml \
  perl-Image-Xpm.noarch \
  libtool-ltdl-devel \
  t1lib \
  t1lib-devel \
  freetype-devel \
  python-setuptools
# Configure Configs and Install PHP7.1
RUN mkdir -p /etc/nginx/conf.d/ssl \
  && mkdir -p /etc/nginx/conf.d/vhosts \
  && mkdir -p /usr/share/nginx/html \
  && mkdir -p /var/www/projects \
  && touch /usr/share/nginx/html/index.php \
  && echo "<?php echo phpinfo(); exit; ?>" >>  /usr/share/nginx/html/index.php \
  && chown -Rf nginx:nginx /usr/share/nginx/html \
  && wget http://sg2.php.net/distributions/php-7.1.25.tar.gz \
  && mkdir -p /usr/local/php7.1 \
  && tar zxvf php-7.1.25.tar.gz \
  && cd php-7.1.25 \
  && ./configure \
  --prefix=/usr/local/php7.1 \
  --enable-fpm \
  --with-mcrypt \
  --enable-mbstring \
  --enable-libxml \
  --with-openssl \
  --with-mysqli \
  --with-mysql-sock \
  --with-gd \
  --with-jpeg-dir=/usr/lib \
  --with-pdo-mysql \
  --with-libxml-dir=/usr/lib \
  --with-xsl \
  --with-mysqli=/usr/bin/mysql_config \
  --with-curl \
  --enable-zip \
  --enable-sockets \
  --with-zlib \
  --enable-exif \
  --enable-ftp \
  --with-iconv \
  --with-gettext \
  --enable-gd-native-ttf \
  --with-freetype-dir=/usr \
  --with-fpm-user=nginx \
  --with-fpm-group=nginx \
  --enable-soap \
  --enable-bcmath \
  --enable-intl \
  --with-libdir=lib64 \
  && make \
  && make install \
  && mkdir -p /usr/local/php7.1/logs \
  && mkdir -p /var/www/projects_7 \
  && cp /root/php-7.1.25/php.ini-development /usr/local/php7.1/lib/php.ini \
  && cp /usr/local/php7.1/etc/php-fpm.d/www.conf.default /usr/local/php7.1/etc/php-fpm.d/www.conf \
  && cp /usr/local/php7.1/etc/php-fpm.conf.default /usr/local/php7.1/etc/php-fpm.conf \
  && ln -s /usr/local/php7.1/etc/php-fpm.conf /etc/php.conf \
  && ln -s /usr/local/php7.1/bin/php /usr/sbin/php \
  && ln -s /usr/local/php7.1/bin/phpize /usr/sbin/phpize \
  && ln -s /usr/local/php7.1/bin/pecl /usr/sbin/pecl \
  && ln -s /usr/local/php7.1/bin/php-config /usr/sbin/php-config \
  && ln -s /usr/local/php7.1/bin/pear /usr/sbin/pear \
  && git clone -b 3.4.x https://github.com/phalcon/cphalcon.git \ 
  && cd cphalcon/build/php7/64bits \
  && /usr/local/php7.1/bin/phpize \
  && ./configure --with-php-config=/usr/local/php7.1/bin/php-config \
  && make \
  && make install \
  && echo "extension=phalcon.so" >> /usr/local/php7.1/lib/php.ini \
  && printf "\n" | pecl install apcu \
  && echo "extension=apcu.so" >> /usr/local/php7.1/lib/php.ini \
  && curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/bin/composer \
  && chmod +x /usr/bin/composer \
  && wget https://github.com/doctrine/migrations/releases/download/v1.0.0/doctrine-migrations.phar \
  && cp doctrine-migrations.phar /usr/bin/doctrine-migrations \
  && chmod 0655 /usr/bin/doctrine-migrations \
  && pecl install mongodb-1.5.3 \
  && echo "extension=mongodb.so" >> /usr/local/php7.1/lib/php.ini \
  && pecl install xdebug \
  && echo "zend_extension=/usr/local/php7.1/lib/php/extensions/no-debug-non-zts-20160303/xdebug.so" >> /usr/local/php7.1/lib/php.ini \
  && echo "xdebug.remote_enable=true" >> /usr/local/php7.1/lib/php.ini \
  && echo "php_flag[display_errors] = on" >> /usr/local/php7.1/etc/php-fpm.conf \
  && printf "\n" | pecl install redis-4.2.0 \
  && echo "extension=redis.so" >> /usr/local/php7.1/lib/php.ini 
COPY config/nginx.conf /etc/nginx/nginx.conf
COPY config/php-fpm	/etc/init.d/php-fpm 
COPY config/www.conf /usr/local/php7.1/etc/php-fpm.d/www.conf 
COPY config/mysql_connector.sh /etc/mysql_connector.sh
# Install Supervisor
RUN curl https://bootstrap.pypa.io/2.6/get-pip.py -o get-pip.py \
  && python get-pip.py \
  && pip install supervisor \
  && chmod +x /etc/init.d/php-fpm \
  && dos2unix /etc/init.d/php-fpm \
  && chmod +x /etc/mysql_connector.sh \
  && dos2unix /etc/mysql_connector.sh
# Install WP-CLI, MySQL Client and Phalcon Debugger
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
  && chmod +x wp-cli.phar \
  && mv wp-cli.phar /usr/local/bin/wp \
  && yum -y install mysql57 \
  && wget --content-disposition https://packagecloud.io/phalcon/stable/packages/el/7/php71u-phalcon-debuginfo-3.4.4-1.ius.el7.x86_64.rpm/download.rpm \
  && yum -y install php71u-phalcon-debuginfo-3.4.4-1.ius.el7.x86_64.rpm

COPY config/supervisord.conf /etc/supervisor/supervisord.conf
WORKDIR /var/www/projects
VOLUME [ "/var/www/projects" ]
CMD ["supervisord"]
