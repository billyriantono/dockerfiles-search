FROM php:7.1-fpm
MAINTAINER Mavdev <miguelangel.valdepenas@aquabluesport.com>

RUN apt-get update \
  && apt-get install -y \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxslt1-dev \
    sendmail-bin \
    sendmail \
    sudo

# Configure the gd library
RUN docker-php-ext-configure \
  gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Install required PHP extensions

RUN docker-php-ext-install \
  dom \
  gd \
  intl \
  mbstring \
  pdo_mysql \
  xsl \
  zip \
  soap \
  bcmath \
  mcrypt

# Install Xdebug (but don't enable)
RUN pecl install -o -f xdebug
RUN pecl install mongodb
RUN echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/mongodb.ini

ENV PHP_MEMORY_LIMIT 2G
ENV PHP_ENABLE_XDEBUG false
ENV MAGENTO_ROOT /var/www/vhosts/magento/current

ENV DEBUG false
ENV UPDATE_UID_GID false

#ADD etc/php-xdebug.ini /usr/local/etc/php/conf.d/zz-xdebug-settings.ini
#ADD etc/mail.ini /usr/local/etc/php/conf.d/zz-mail.ini

#ADD docker-entrypoint.sh /docker-entrypoint.sh

#RUN ["chmod", "+x", "/docker-entrypoint.sh"]

#ENTRYPOINT ["/docker-entrypoint.sh"]

ENV MAGENTO_RUN_MODE developer
ENV UPLOAD_MAX_FILESIZE 64M

#ADD etc/php-fpm.ini /usr/local/etc/php/conf.d/zz-magento.ini

#ADD etc/php-fpm.conf /usr/local/etc/

#CMD ["php-fpm", "-F"]

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod a+x /usr/local/bin/composer

RUN apt-get remove -y openssh-server
RUN apt-get install -y openssh-server

#ssh
#RUN echo “root:training” | chpasswd
#RUN sed -i ‘s/prohibit-password/yes/’ /etc/ssh/sshd_config
#ADD ssh.tar /root/
#RUN chown -R root:root /root/.ssh;chmod -R 700 /root/.ssh
RUN echo "StrictHostKeyChecking=no" >> /etc/ssh/ssh_config
RUN mkdir /var/run/sshd

EXPOSE 2020
