FROM php:7.3-alpine


RUN apk --no-cache add git openssh bash nodejs-npm yarn rsync make postgresql-client

# Install php lib
RUN set -eux; \
    apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    gettext-dev \
    icu-dev \
    postgresql-dev \
    libzip-dev \
    ; \
    docker-php-ext-install \
    gettext \
    intl \
    pcntl \
    pdo_pgsql \
    zip \
    bcmath \
    ;\
    runDeps="$( \
    scanelf --needed --nobanner --format '%n#p' --recursive /usr/local/lib/php/extensions \
    | tr ',' '\n' \
    | sort -u \
    | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
    )"; \
    apk add --no-cache --virtual .phpexts-rundeps $runDeps; \
    \
    apk del .build-deps

RUN echo "memory_limit=-1" > "$PHP_INI_DIR/conf.d/memory-limit.ini" \
 && echo "date.timezone=${PHP_TIMEZONE:-UTC}" > "$PHP_INI_DIR/conf.d/date_timezone.ini"

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
ENV COMPOSER_CACHE_DIR=/tmp/.docker_composer
ENV COMPOSER_MEMORY_LIMIT=-1
ENV COMPOSER_ALLOW_SUPERUSER 1

# Install PHPUnit
RUN curl -SL "https://phar.phpunit.de/phpunit-8.phar" -o /usr/local/bin/phpunit \
	&& chmod +x /usr/local/bin/phpunit

RUN npm i -g eclint bower grunt --cache /tmp/npm-cache

RUN mkdir -p ~/.ssh
RUN echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config

WORKDIR /app

CMD ["echo"]
