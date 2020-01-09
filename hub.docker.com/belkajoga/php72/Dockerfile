FROM fedora:29
LABEL version="0.1"
RUN dnf -y update && \
    dnf -y install  \
    patch \
    git \
    unzip \
    php-bcmath \
    php \
    php-mbstring \
    php-pear \
    gd \
    php-gd \
    ImageMagick \
    php-intl \
    php-mbstring \
    mcrypt \
    php-mcrypt \
    mhash \
    openssl \
    php-soap \
    php-xml \
    zip \
    php-pecl-zip \
    php-json \
    php-pecl-xdebug \
    php-mysqlnd \
    php-fpm && \
  curl -sS https://getcomposer.org/installer | php && \  
  mv composer.phar /usr/local/bin/composer && \
  mkdir /run/php-fpm && \
  chown root:apache /var/lib/php/session && \
  chmod 770 /var/lib/php/session && \
  dnf clean all 

EXPOSE 9000
VOLUME /var/www/html
VOLUME /usr/share/httpd/.composer
RUN chown apache:apache /usr/share/httpd/.composer
WORKDIR /var/www/html
RUN chown apache:apache /var/www/html
RUN chmod g+s /var/www/html

ENV PHP_INI memory_limit=2048M&date.timezone="Europe/London" 
ENV FPM listen=9000&listen.allowed_clients&pm=static&pm.max_children=8&user=root&group=root
ENV XDEBUG=zend_extension=xdebug.so&xdebug.remote_port=9000&xdebug.remote_enable=1&xdebug.remote_connect_back=0&xdebug.remote_handler=dbgp&xdebug.idekey=PHPSTORM&xdebug.remote_host=host.docker.internal

COPY conf/startService.sh /usr/local/bin
RUN chmod +x /usr/local/bin/startService.sh

ENTRYPOINT [ "/usr/local/bin/startService.sh" ]
