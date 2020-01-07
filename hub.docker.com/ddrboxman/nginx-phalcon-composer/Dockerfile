FROM debian:wheezy

RUN apt-get update && apt-get -y install \
  git \
  nginx-extras \
  php5-cli \
  php5-dev \
  php5-fpm \
  libpcre3-dev \
  gcc \
  make \
  php5-mysql \
  curl \
  php5-curl

RUN git clone --depth=1 http://github.com/phalcon/cphalcon.git -b 1.2.3 cphalcon
RUN cd cphalcon/build && ./install;

RUN echo 'extension=phalcon.so' >> /etc/php5/fpm/conf.d/30-phalcon.ini

RUN curl -sS https://getcomposer.org/installer | php && \
  mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer && \
  composer global require 'phpunit/phpunit=3.7.*' && \
  echo "export PATH=$PATH:/.composer/vendor/bin/:" >> /root/.profile

ADD nginx.conf /etc/nginx/nginx.conf
ADD default /etc/nginx/sites-available/default

RUN mkdir /var/www
RUN echo "<?php phpinfo(); ?>" > /var/www/index.php

EXPOSE 80

CMD service php5-fpm start && nginx
