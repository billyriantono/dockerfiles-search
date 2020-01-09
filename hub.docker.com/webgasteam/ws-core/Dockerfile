FROM php:5.6-apache
COPY config/php.ini /usr/local/etc/php/

RUN apt-get update && apt-get install -y \
       libfreetype6-dev \
       libjpeg62-turbo-dev \
       libmcrypt-dev \
       libpng12-dev \
       libicu-dev \
       locales \
       netcat \
       mysql-client \
       git \
       unzip \
       phpunit \
       php5-curl \
       php5-mysql \
       cron \
       vim


RUN a2enmod rewrite

RUN docker-php-ext-install pdo pdo_mysql mysql
RUN docker-php-ext-install mbstring mcrypt

RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php
RUN php composer-setup.php --install-dir=/usr/bin/ --filename=composer
RUN php -r "unlink('composer-setup.php');"

ENV APP_ENV=${APP_ENV:-"local"}
ENV APP_URL=${APP_URL:-"http://localhost"}
ENV APP_DEBUG=${APP_DEBUG:-"true"}
ENV APP_KEY=${APP_KEY:-"SFRWUOicJQk3WeUE8GgyPDEmMvVpp7BI"}
ENV APP_TIMEZONE=${APP_TIMEZONE:-"America/Sao_Paulo"}
ENV PHP_ERROR_REPORTING=${PHP_ERROR_REPORTING:-"E_ALL & ~E_NOTICE"}
ENV PHP_XDEBUG=${PHP_XDEBUG:-"false"}

RUN sed -i "s#{{PHP_ERROR_REPORTING}}#$PHP_ERROR_REPORTING#g" /usr/local/etc/php/php.ini

ENV DB_HOST=${DB_HOST:-"mysql"}
ENV DB_PORT=${DB_PORT:-"3306"}
ENV DB_USERNAME=${DB_USERNAME:-"root"}
ENV DB_DATABASE=${DB_DATABASE:-"ws-core"}
ENV DB_PASSWORD=${DB_PASSWORD:-"secret"}

ENV FACEBOOK_APP_ID=${FACEBOOK_APP_ID:-"614354835397939"}
ENV FACEBOOK_APP_SECRET=${FACEBOOK_APP_SECRET:-"b66e5fa2c3194aeb9756e10574111c97"}

ENV GOOGLE_MAPS_API_KEY=${GOOGLE_MAPS_API_KEY:-"AIzaSyCt8a28RmXYAyeSXoLKV9DkkYcfCDvGr2o"}

ENV CACHE_DRIVER=${CACHE_DRIVER:-"file"}
ENV SESSION_DRIVER=${SESSION_DRIVER:-"file"}
ENV QUEUE_DRIVER=${QUEUE_DRIVER:-"sync"}

ENV REDIS_HOST=${REDIS_HOST:-"127.0.0.1"}
ENV REDIS_PASSWORD=${REDIS_PASSWORD:-"null"}
ENV REDIS_PORT=${REDIS_PORT:-"6379"}

ENV MAIL_DRIVER=${MAIL_DRIVER:-"smtp"}
ENV MAIL_HOST=${MAIL_HOST:-"mailtrap.io"}
ENV MAIL_PORT=${MAIL_PORT:-"2525"}
ENV MAIL_USERNAME=${MAIL_USERNAME:-"no-replay@domain.com"}
ENV MAIL_PASSWORD=${MAIL_PASSWORD:-"secret"}
ENV MAIL_ENCRYPTION=${MAIL_ENCRYPTION:-"tls"}

ENV OAUTH_BITBUCKET_KEY=${OAUTH_BITBUCKET_KEY:-"wQRgxaYJSSs5LL8UKe"}
ENV OAUTH_BITBUCKET_SECRET=${OAUTH_BITBUCKET_SECRET:-"W8Jk3e5LDxFMaVFbX3MnM7h9Hprp2LSe"}

ENV COMPOSER_UPDATE=${COMPOSER_UPDATE:-"false"}
ENV RESTORE_INITIAL_DATABASE=${RESTORE_INITIAL_DATABASE:-"false"}

RUN echo '* * * * * /usr/bin/php /var/www/html/artisan schedule:run >> /dev/null 2>&1' >> /etc/crontab

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
COPY environment-setup.sh /environment-setup.sh
RUN chmod +x /environment-setup.sh
COPY database/db-dump-ws-core.sql.zip /tmp/db-dump-ws-core.sql.zip

# grr, ENTRYPOINT resets CMD now
ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2-foreground"]