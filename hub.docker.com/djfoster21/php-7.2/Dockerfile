FROM ubuntu:bionic

LABEL version="0.1"
LABEL description="A simple PHP 7.2 Server"

ENV TERM=linux

RUN apt-get update \
    && apt-get install -y --no-install-recommends gnupg \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu bionic main" > /etc/apt/sources.list.d/ondrej-php.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C \
    && apt-get update \
    && apt-get -y --no-install-recommends install \
        curl ca-certificates unzip \
        php7.2-cli \
        php7.2-curl \
        php-apcu \
        php-apcu-bc \
        php7.2-json \
        php7.2-mbstring \
        php7.2-opcache \
        php7.2-readline \
        php7.2-xml \
        php7.2-zip \
        php7.2-fpm \
        php-memcached \
        php7.2-mysql \ 
        php-xdebug \
        php7.3-gd \
    && curl -sL https://deb.nodesource.com/setup_10.x | bash -\
    && apt-get install -y --no-install-recommends nodejs \
    && apt-get install -y --no-install-recommends git ssh \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* 

# Install composer && laravel installer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer\
    && php -r "unlink('composer-setup.php');" \
    && composer global require hirak/prestissimo \    
    && composer global require laravel/installer \
    && composer global require friendsofphp/php-cs-fixer \
    && composer global require phpunit/phpunit \
    && composer global require "squizlabs/php_codesniffer=*" \
    && composer global require phpmd/phpmd \
    && composer clear-cache 

COPY custom.conf /etc/php/7.2/fpm/pool.d/z-custom.conf    
COPY config.ini /etc/php/7.2/fpm/pool.d/98-overrides.ini
# Add composer bin to path    
RUN  echo "export PATH=\$HOME/.composer/vendor/bin:\$PATH" >> ~/.bashrc    

RUN mkdir -p /run/php/ 
CMD /usr/sbin/php-fpm7.2 -F -O
EXPOSE 9000