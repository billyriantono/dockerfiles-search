FROM chilio/laravel-dusk-ci:stable

RUN php -i | grep "Loaded Configuration File"

# Install composer
ENV COMPOSER_HOME /composer
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

# Install Firebase
RUN apt-get update
RUN apt-get install -y autoconf libz-dev php7.2-dev php-pear
RUN pecl install grpc
RUN echo 'extension=grpc.so' > /etc/php/7.2/cli/php.ini
