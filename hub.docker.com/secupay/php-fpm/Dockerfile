FROM debian:jessie
MAINTAINER Nicolas Wild <nwild79@gmail.com>

# Prepare
RUN apt-get update -qq \
    && apt-get install -qy --force-yes wget \
    && apt-get install -qy --force-yes git \
    && apt-get install -qy --force-yes unzip

# Install PHP
RUN apt-get install -qy --force-yes \
    php5 \
    php5-dev \
    php5-xdebug \
    php5-xsl \
    php5-intl \
    php5-curl \
    php5-mysql \
    php5-mcrypt \
    php5-pgsql \
    php5-sqlite \
    php5-fpm \
    php5-apcu \
    php5-ldap \
    php5-gd \
    php-pear \
    && mkdir -p /var/log/php5-fpm

# Install PHP Extension AMQP
ENV PHP_AMQP_VERSION 1.6.1

#RUN apt-get install -qy --force-yes \
#        re2c \
#        amqp-tools \
#        librabbitmq-dev \
#    && cd /opt \
#    && wget https://pecl.php.net/get/amqp-$PHP_AMQP_VERSION.tgz -O amqp.tar.gz \
#    && tar -zxvf amqp.tar.gz \
#    && rm -f amqp.tar.gz \
#    && cd amqp-$PHP_AMQP_VERSION \
#    && phpize \
#    && ./configure --with-amqp \
#    && make \
#    && make install \
#    && echo "extension=amqp.so" > /etc/php5/mods-available/amqp.ini \
#    && php5enmod amqp

# librabbitmq-dev is too old, have to use https://github.com/alanxz/rabbitmq-c/releases/download/v0.7.1/rabbitmq-c-0.7.1.tar.gz

# Install PHP Extension Cassandra
RUN apt-get install -qy --force-yes \
        g++ \
        make \
        cmake \
        libuv-dev \
        libssl-dev \
        libgmp-dev \
        openssl \
        libpcre3-dev \
    && cd /opt \
    && git clone https://github.com/datastax/php-driver.git \
    && cd php-driver \
    && git submodule update --init \
    && cd ext \
    && ./install.sh \
    && cp cassandra.ini /etc/php5/mods-available \
    && php5enmod cassandra

# config PHP-FPM
#RUN sed -i 's/listen = \/var\/run\/php5-fpm.sock/listen = 0.0.0.0:9000/g' /etc/php5/fpm/pool.d/www.conf \
#    && sed -i "s/error_log = \/var\/log\/php5-fpm.log/error_log = \/var\/log\/php5-fpm\/error.log/" /etc/php5/fpm/php-fpm.conf \
#    && sed -i "s/user = www-data/user = root/" /etc/php5/fpm/pool.d/www.conf \
#    && sed -i "s/group = www-data/group = root/" /etc/php5/fpm/pool.d/www.conf \
#    && sed -i "s/listen.owner = www-data/listen.owner = root/" /etc/php5/fpm/pool.d/www.conf \
#    && sed -i "s/listen.group = www-data/listen.group = root/" /etc/php5/fpm/pool.d/www.conf



# Install IonCube Loader (Required by XtCommerce)
RUN mkdir -p /tmp/install/ && \
    cd /tmp/install && \
    wget http://downloads2.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.zip && \
    unzip ioncube_loaders_lin_x86-64.zip && \
    mv ioncube/ioncube_loader_lin_5.6.so $(php-config --extension-dir)/ioncube_loader.so && \
    rm -rf /tmp/install




WORKDIR /www

COPY ./conf/php.ini /etc/php5/fpm/
COPY ./conf/php-fpm.conf /etc/php5/fpm/
COPY ./conf/php-fpm.conf.default /etc/php5/fpm/
COPY ./conf/pool.d/* /etc/php5/fpm/pool.d/


# Enable ioncube
# insert a new line and add the extension to php.ini
RUN echo >> /etc/php5/fpm/php.ini && \
    echo "zend_extension=$(php-config --extension-dir)/ioncube_loader.so" >> /etc/php5/fpm/php.ini


VOLUME /var/log
VOLUME /www

EXPOSE 9000-9999

ENTRYPOINT ["php5-fpm","-F"]
