FROM fncmedia/php-fpm:5.6

ENV COMPOSER_VERSION 1.1.2

ENV NODE_VERSION=9

ENV XDEBUG_VERSION 2.3.3


# Environment Layer
RUN php -r "copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');" \
    && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION} \
    && rm -rf /tmp/composer-setup.php


RUN cd /tmp \
    && wget -qO- http://xdebug.org/files/xdebug-$XDEBUG_VERSION.tgz | tar zx \
    && cd /tmp/xdebug-$XDEBUG_VERSION \
    && phpize \
    && ./configure \
    && make -j \
    && make install \
    && rm -rf "/tmp/xdebug-$XDEBUG_VERSION"

RUN touch /usr/local/etc/php/conf.d/xdebug.ini; \
    echo "zend_extension = $(find /usr/local/lib/php/extensions/ -name xdebug.so)" >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo "xdebug.remote_autostart=0" >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo "xdebug.remote_log=/tmp/php5-xdebug.log" >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo "memory_limit=256M" > /usr/local/etc/php/conf.d/limits.ini


#RUN touch /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini; \
#  	echo "opcache.validate_timestamps=0" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini;

# Install dependencies
RUN apt-get -y update \
    && apt-get install -y gnupg \
    && wget -qO- https://deb.nodesource.com/setup_$NODE_VERSION.x | bash -  && apt-get install -y \
      git \
      nodejs \
      vim \
      ruby \
      ruby-dev \
      nano \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get -y clean

RUN gem install sass --no-user-install

RUN npm install -g bower

