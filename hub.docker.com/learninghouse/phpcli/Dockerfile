FROM alpine:3.8
LABEL Maintainer="Michael Bunch <mbunch@learninghouse.com>"

ENV PHP_VERSION 7
ENV PHP_CONFIG_DIR /etc/php7

# Install PHP
RUN apk --no-cache add \
    curl \
    php7 \
    php7-ctype \
    php7-curl \
    php7-dom \
    php7-fileinfo \
    php7-json \
    php7-mbstring \
    php7-mcrypt \
    php7-opcache \
    php7-pdo_mysql \
    php7-phar \
    php7-session \
    php7-tokenizer \
    php7-zip \
    git

# Setup application user/group/cwd
RUN adduser -D -g 'www' www && \
    mkdir -p /app && \
    chown -R www:www /app
WORKDIR /app

# Configure PHP logging
RUN mkdir /var/log/php${PHP_VERSION} && \
    mkfifo -m 666 /var/log/php${PHP_VERSION}/stdout && \
    mkfifo -m 666 /var/log/php${PHP_VERSION}/stderr

# Install Composer
COPY scripts/install_composer.sh /root
RUN chmod 755 /root/install_composer.sh && \
    cd /root && \
    ./install_composer.sh
ENV PATH="/root/.composer/vendor/bin:${PATH}"
RUN composer global require hirak/prestissimo && \
    rm -rf /root/.composer/cache

# Setup container runtime
COPY scripts/entrypoint.sh /sbin/entrypoint.sh
COPY scripts/export_secrets.sh /sbin/export_secrets
COPY scripts/optimize_laravel.sh /sbin/optimize_laravel
RUN chmod 755 /sbin/entrypoint.sh && \
    chmod 755 /sbin/export_secrets && \
    chmod 755 /sbin/optimize_laravel

CMD ["/sbin/entrypoint.sh"]
