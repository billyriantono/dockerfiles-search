FROM php:7.2-apache

ENV APP_DIR /var/proteinscreener

RUN apt-get update && \
    apt-get install -y gnupg2 sqlite3 unzip && \
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install --no-install-recommends -y nodejs build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /tmp
ENV COMPOSER_VERSION 1.6.3

RUN curl -s -f -L -o /tmp/installer.php https://raw.githubusercontent.com/composer/getcomposer.org/b107d959a5924af895807021fcef4ffec5a76aa9/web/installer \
 && php -r " \
    \$signature = '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061'; \
    \$hash = hash('SHA384', file_get_contents('/tmp/installer.php')); \
    if (!hash_equals(\$signature, \$hash)) { \
        unlink('/tmp/installer.php'); \
        echo 'Integrity check failed, installer is either corrupt or worse.' . PHP_EOL; \
        exit(1); \
    }" \
 && php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer --version=${COMPOSER_VERSION} \
 && composer --ansi --version --no-interaction \
 && rm -rf /tmp/* /tmp/.htaccess
 
COPY . $APP_DIR

WORKDIR $APP_DIR

RUN npm install

RUN npm run build

RUN rm -rf node_modules

RUN composer install --no-dev && \
    composer dumpautoload -o
    
COPY .env.example .env

RUN > database/database.sqlite

RUN chmod -R a+w storage/logs database

COPY public/config.example.json public/config.json

RUN rm -rf /var/www/html && \
    ln -s $APP_DIR/public /var/www/html
    
RUN a2enmod rewrite

CMD php artisan migrate --force && apachectl -D FOREGROUND

EXPOSE 80
