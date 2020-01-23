ARG VERSION=latest

FROM php:$VERSION

# add os packages and docker cli
RUN apt-get update && apt-get install -y python3-dev netcat gnupg2 gnupg-agent libjpeg-dev libpng-dev git curl unzip jq gosu apt-transport-https ca-certificates ssl-cert build-essential software-properties-common lsb-release \
    && curl -fsSL https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/gpg | apt-key add - 2>/dev/null \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]') $(lsb_release -cs) stable" \
    && apt-get update \
    && apt-get install -y docker-ce-cli

# add vaultenv and wait-for
ADD https://github.com/gendall/vaultenv/releases/download/v0.11.0/vaultenv /usr/local/bin/vaultenv
ADD https://raw.githubusercontent.com/gendalldesign/wait-for/master/wait-for /usr/local/bin/wait-for
RUN chmod +x /usr/local/bin/vaultenv /usr/local/bin/wait-for && ln -s /run/secrets/vault_config /etc/vaultenv.conf

# set environment variables
ENV PHP_ENV=development NODE_ENV=development PUBLIC_DIR=html VAULTENV_SECRETS_FILE=/run/secrets/vault_secrets

# install composer
RUN curl -sL https://raw.githubusercontent.com/composer/getcomposer.org/5eb0614d3fa7130b363698d3dca52c619b463615/web/installer | php -- --quiet && \
    mv composer.phar /usr/local/bin/composer 

# install apache modules
RUN a2enmod rewrite expires ssl

# install php extensions
RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
    docker-php-ext-install gd pdo_mysql mysqli opcache zip

# install xdebug
ARG VERSION=latest
RUN ["/bin/bash", "-c", \
    "XDEBUG=$([[ $VERSION = 7* ]] && echo xdebug-2.6.1 || echo xdebug-2.5.5) && \
    yes | pecl install $XDEBUG"]
    
# create sessions directory and copy base config
RUN install -d -m 0755 -o www-data -g www-data /var/lib/php/session
COPY php.*.ini /opt/php/
COPY httpd.conf /etc/apache2/sites-enabled/000-default.conf

COPY entrypoint.sh /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 80 443
CMD ["apache2-foreground"]
