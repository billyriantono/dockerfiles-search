FROM php:7.1-fpm

# dependencies
RUN apt-get update && apt-get install -y curl git openssh-client zlib1g-dev
RUN docker-php-ext-install zip

# composer
ENV COMPOSER_VERSION 1.5.6
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
    && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
    && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
    && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION} \
    && rm -f /tmp/composer-setup.php /tmp/composer-setup.sig

# nginx
RUN apt-get update && apt-get install -y nginx
COPY nginx.conf /etc/nginx/nginx-custom.conf
RUN echo 'fastcgi_param  HTTP_USER_AGENT    $http_user_agent;' >> /etc/nginx/fastcgi_params

# entry
COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN ["chmod", "+x", "/usr/local/bin/entrypoint.sh"]
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
