FROM php:7.3.8-apache

RUN apt-get update && apt-get install -y \
    git \
    zlib1g-dev \
    unixodbc \
    unixodbc-dev \
    freetds-dev \
    freetds-bin \
    tdsodbc \
    libicu-dev &&\
    rm -rf /var/lib/apt/lists/*;

# Set timezone
RUN rm /etc/localtime &&\
    ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime &&\
    "date"

RUN set -x \
    && cd /usr/src/ && tar -xf php.tar.xz && mv php-7* php \
    && cd /usr/src/php/ext/odbc \
    && phpize \
    && sed -ri 's@^ *test +"\$PHP_.*" *= *"no" *&& *PHP_.*=yes *$@#&@g' configure \
    && ./configure --with-unixODBC=shared,/usr > /dev/null \
    && docker-php-ext-install odbc > /dev/null

RUN apt-get update

# xDEBUG testing 
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
RUN echo 'xdebug.remote_enable=on' >> /usr/local/etc/php/conf.d/xdebug.ini 
RUN echo 'xdebug.remote_host=10.0.75.1' >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo 'xdebug.remote_port=9000' >> /usr/local/etc/php/conf.d/xdebug.ini
RUN a2enmod rewrite 


RUN apt-get install -y libpq-dev && \
    apt-get install -y libpng-dev && \
    apt-get install -y zip unzip && \
    apt-get install -y git && \
    docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql && \
    docker-php-ext-install pdo pdo_pgsql pgsql && \
    docker-php-ext-install gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer    

RUN a2enmod rewrite
RUN a2enmod headers    

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo intl mbstring
RUN docker-php-ext-configure pdo_dblib --with-libdir=/lib/x86_64-linux-gnu

#XDEBUG 
RUN docker-php-ext-install pdo_dblib
RUN docker-php-ext-enable intl mbstring pdo_dblib
