FROM alpine:3.5

ENV PATH "/composer/vendor/bin:$PATH"
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV COMPOSER_VERSION 1.4.2

RUN apk --no-cache add \
    curl git openssh openssl bash \
    php7 php7-ctype php7-curl php7-dom php7-fpm php7-json php7-mbstring php7-opcache php7-openssl php7-pdo_mysql php7-phar php7-session php7-zlib && \
  ln -s /usr/bin/php7 /usr/bin/php && \
  echo "memory_limit=-1" > "/etc/php7/conf.d/memory-limit.ini" && \
  echo "date.timezone=Africa/Johannesburg" > "/etc/php7/conf.d/date_timezone.ini" && \
  curl -s -f -L -o /tmp/installer.php https://raw.githubusercontent.com/composer/getcomposer.org/5fd32f776359b8714e2647ab4cd8a7bed5f3714d/web/installer && \
  php -r " \
    \$signature = '55d6ead61b29c7bdee5cccfb50076874187bd9f21f65d8991d46ec5cc90518f447387fb9f76ebae1fbbacf329e583e30'; \
    \$hash = hash('SHA384', file_get_contents('/tmp/installer.php')); \
    if (!hash_equals(\$signature, \$hash)) { \
        unlink('/tmp/installer.php'); \
        echo 'Integrity check failed, installer is either corrupt or worse.' . PHP_EOL; \
        exit(1); \
    }" && \
  php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer --version=${COMPOSER_VERSION} && \
  rm /tmp/installer.php && \
  composer --ansi --version --no-interaction && \
  composer global require "hirak/prestissimo:^0.3"

WORKDIR /var/www/html
