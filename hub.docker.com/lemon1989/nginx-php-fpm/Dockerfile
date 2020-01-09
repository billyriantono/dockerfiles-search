FROM richarvey/nginx-php-fpm:latest

LABEL MAINTAINER="452664116@qq.com"

LABEL Name=nginx-php-fpm-with-phalcon
LABEL Version=0.0.1

# install some packages and phalcon
RUN apk --no-cache add php7-dev autoconf  g++ gcc make libc-dev re2c file\
  && cd /home \
  && git clone -b 3.4.x --depth=1 git://github.com/phalcon/cphalcon.git \ 
  && cd cphalcon/build \
  && ./install --phpize /usr/local/bin/phpize --php-config /usr/local/bin/php-config \
  && echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini \
  && cd /home && rm -rf ./cphalcon
  
  
# install redis extension  
RUN mkdir -p /tmp/redis \
  && cd /home \
  && wget https://github.com/phpredis/phpredis/archive/3.0.0.tar.gz \
  && tar zxvf 3.0.0.tar.gz -C /tmp/redis --strip 1 \
  && docker-php-ext-configure /tmp/redis --enable-redis \
  && docker-php-ext-install /tmp/redis \
  && rm -r /tmp/redis \
  && cd /home && rm -rf ./3.0.0.tar.gz

# remove not needed files
RUN apk del php7-dev autoconf  g++ gcc make libc-dev re2c \
  && rm -rf /var/cache/apk/*

RUN supervisorctl restart php-fpm