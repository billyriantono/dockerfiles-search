FROM php:7.3-apache

# Install PHP extensions
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get update && apt-get install -y libicu-dev libpq-dev libmcrypt-dev \
      mysql-client ruby-full nodejs \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-install intl mbstring mysqli pdo_mysql pdo_pgsql

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# SASS compiler
RUN su -c "gem install sass"

# Install Xdebug
#RUN curl -fsSL 'https://xdebug.org/files/xdebug-2.4.0.tgz' -o xdebug.tar.gz \
#    && mkdir -p xdebug \
#    && tar -xf xdebug.tar.gz -C xdebug --strip-components=1 \
#    && rm xdebug.tar.gz \
#    && ( \
#    cd xdebug \
#    && phpize \
#    && ./configure --enable-xdebug \
#    && make -j$(nproc) \
#    && make install \
#    ) \
#    && rm -r xdebug \
#    && docker-php-ext-enable xdebug

#Xdebug
RUN pecl install xdebug-2.7.0
RUN docker-php-ext-enable xdebug
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini


# Put apache config
#COPY build/apache-vhost.conf /etc/apache2/sites-available/custom-vhost.conf
#RUN a2dissite 000-default.conf && a2ensite custom-vhost.conf && a2enmod rewrite

# Change uid and gid of apache to docker user uid/gid
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

WORKDIR /var/www/html