FROM php:7.1-fpm

RUN apt-get update && apt-get install -y libmcrypt-dev
RUN apt-get install -y vim cron supervisor
RUN docker-php-ext-install mbstring pdo_mysql tokenizer

RUN apt-get install -y libssl-dev pkg-config

RUN pecl install mongodb
RUN echo "extension=mongodb.so" >> /usr/local/etc/php/conf.d/mongodb.ini


RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng12-dev \
	&& docker-php-ext-install -j$(nproc) iconv mcrypt \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install pcntl \
	&& docker-php-ext-configure pcntl

RUN apt-get purge nodejs npm
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs git rsync zip unzip mysql-client

RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

RUN apt-get install -yq python ca-certificates
RUN curl -O https://bootstrap.pypa.io/get-pip.py && python get-pip.py
RUN pip install awsebcli awscli

RUN mkdir ~/.aws/ && touch ~/.aws/credentials && touch ~/.aws/config

CMD supervisord -c /etc/supervisor/supervisord.conf && supervisorctl reload && php-fpm