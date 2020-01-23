FROM php:5-fpm
MAINTAINER Lars S. Linnet <lars@adapt.dk>

RUN \
    apt-get update && apt-get install -y \
      libfreetype6-dev \
      libjpeg62-turbo-dev \
      libmcrypt-dev \
      libpng12-dev \
      msmtp \
      mariadb-client \
      htop \
      php5-xdebug \
    && docker-php-ext-install -j$(nproc) \
      iconv \
      mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure mbstring --enable-mbstring \
    && docker-php-ext-install -j$(nproc) \
      gd \
      pdo \
      pdo_mysql \
      mbstring \
    && docker-php-ext-install -j$(nproc) \
      pcntl \
      zip \
      opcache \
      mcrypt

# Possible values for docker-php-ext-install:
# bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp hash
# iconv imap interbase intl json ldap mbstring mcrypt mssql mysql mysqli oci8 odbc opcache pcntl
# pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix
# pspell readline recode reflection session shmop simplexml snmp soap sockets spl standard
# sybase_ct sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zip

RUN \
  mkdir /run/php/ && \
  chown www-data: /run/php/ && \
  touch /var/log/fpm-php.www.log && \
  chown www-data: /var/log/fpm-php.www.log

RUN \
  php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php -r "if (hash_file('SHA384', 'composer-setup.php') === '070854512ef404f16bac87071a6db9fd9721da1684cd4589b1196c3faf71b9a2682e2311b36a5079825e155ac7ce150d') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php composer-setup.php --version=1.1.2 --filename=composer --install-dir=/usr/local/bin && \
  php -r "unlink('composer-setup.php');"

RUN \
  mkdir --parents /opt/drush-8.x && \
  cd /opt/drush-8.x && \
  composer init --require=drush/drush:8.* -n && \
  composer config bin-dir /usr/local/bin && \
  composer install

RUN \
  apt-get clean && \
  rm -r /var/lib/apt/lists/*

COPY files/etc/ /etc/

EXPOSE 9000
