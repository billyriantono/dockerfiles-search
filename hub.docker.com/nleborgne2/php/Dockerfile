FROM php:7.2.16-fpm

ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/79a255bd8c41cd6dbfc54f9ca75950bb4f80a63d/install-php-extensions /usr/local/bin/
RUN chmod uga+x /usr/local/bin/install-php-extensions

RUN install-php-extensions gd imagick intl pdo_mysql pdo_pgsql zip

RUN apt-get update && apt-get install --yes git unzip cron
COPY --from=composer:1.8.5 /usr/bin/composer /usr/bin/composer

ADD https://phar.phpunit.de/phpunit-6.5.14.phar /usr/local/bin/phpunit
RUN chmod a+rx /usr/local/bin/phpunit

RUN apt-get update && \
    apt-get install -y build-essential libsasl2-dev libssl-dev python-minimal && \
    cd /tmp && \
    git clone \
        --branch v0.11.5 \
        --depth 1 \
        https://github.com/edenhill/librdkafka.git && \
    cd librdkafka && \
    ./configure && \
    make && \
    make install && \
    pecl install rdkafka && \
    docker-php-ext-enable rdkafka && \
    rm -rf /tmp/librdkafka && \
    apt-get purge \
        -y --auto-remove \
        -o APT::AutoRemove::RecommendsImportant=false \
        build-essential libsasl2-dev libssl-dev python-minimal

RUN curl --output /tmp/datadog-php-tracer_amd64.deb --location https://github.com/DataDog/dd-trace-php/releases/download/0.27.2/datadog-php-tracer_0.27.2_amd64.deb && \
    apt-get install /tmp/datadog-php-tracer_amd64.deb && \
    rm /tmp/datadog-php-tracer_amd64.deb

RUN apt-get update || apt-get update && apt-get install -y chromium

RUN mkdir -p /tmp/blackfire \
    && curl -A "Docker" -L https://blackfire.io/api/v1/releases/client/linux_static/amd64 | tar zxp -C /tmp/blackfire \
    && mv /tmp/blackfire/blackfire /usr/bin/blackfire \
    && rm -Rf /tmp/blackfire

RUN version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/$version \
    && mkdir -p /tmp/blackfire \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp/blackfire \
    && mv /tmp/blackfire/blackfire-*.so $(php -r "echo ini_get ('extension_dir');")/blackfire.so \
    && printf "extension=blackfire.so\nblackfire.agent_socket=tcp://blackfire:8707\n" > $PHP_INI_DIR/conf.d/blackfire.ini \
    && rm -rf /tmp/blackfire /tmp/blackfire-probe.tar.gz

RUN pecl install xdebug && docker-php-ext-enable xdebug

RUN echo 'memory_limit=1G' > /usr/local/etc/php/conf.d/docker.ini

ENV PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/ssl/bin"
ENV XDG_CACHE_HOME="/home/user/.cache"
