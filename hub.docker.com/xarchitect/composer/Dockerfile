FROM xarchitect/php:latest

RUN mkdir -p /var/www/default

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN chmod 755 /usr/bin/composer
RUN apt-get install -y git
RUN /usr/bin/composer global require hirak/prestissimo

WORKDIR /var/www/default
ENTRYPOINT ["/usr/bin/composer"]
