FROM alpine

ENV WORDPRESS_LANG=pt_BR
ENV LANG=br
ENV DATABASE_NAME=wordpress
ENV DATABASE_USER=wordpress
ENV DATABASE_PASS=1234
ENV DATABASE_HOST=
ENV DOMAIN=localhost
ENV TITLE=Wordrpess
ENV WORDPRESS_ADMIN=admin
ENV WORDPRESS_PASS=clnadm9
ENV WORDPRESS_EMAIL=admin@admin

ENV WORDPRESS_CLI_GPG_KEY 63AF7AA15067C05616FDDD88A3A2E8F226F0BC06
ENV WORDPRESS_CLI_VERSION 2.4.0
ENV WORDPRESS_CLI_SHA512 4049c7e45e14276a70a41c3b0864be7a6a8cfa8ea65ebac8b184a4f503a91baa1a0d29260d03248bc74aef70729824330fb6b396336172a624332e16f64e37ef

RUN apk update && apk upgrade
RUN apk add apache2
RUN apk add \
    less \
    git \
    apache2 \
    bash \
    ca-certificates \
    curl \
    nano \
    openntpd \
    openssh \
    openssl \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    mariadb-client \
    mysql-client \
    php7 \
    php7-apache2 \
    php7-apcu \
    php7-bcmath \
    php7-bz2 \
    php7-ctype \
    php7-curl \
    php7-dom \
    php7-exif \
    php7-fileinfo \
    php7-ftp \
    php7-gd \
    php7-gettext \
    php7-gmp \
    php7-iconv \
    php7-intl \
    php7-json \
    php7-ldap \
    php7-mbstring \
    php7-mcrypt \
    php7-mysqli \
    php7-odbc \
    php7-openssl \
    php7-pdo \
    php7-pdo_dblib \
    php7-pdo_mysql \
    php7-pdo_odbc \
    php7-pdo_pgsql \
    php7-pdo_sqlite \
    php7-phar \
    php7-redis \
    php7-session \
    php7-simplexml \
    php7-soap \
    php7-sqlite3 \
    php7-tokenizer \
    php7-xdebug \
    php7-xml \
    php7-xmlreader \
    php7-xmlrpc \
    php7-xmlwriter \
    php7-zip \
    unzip \
    tzdata \
    freetype-dev \
    imagemagick-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libzip-dev 

RUN mkdir -p /var/www/html && chown -R apache:apache /var/www/html && chmod -R 755 /var/www/html
WORKDIR /var/www/html

RUN sed -i "s/#LoadModule\ rewrite_module/LoadModule\ rewrite_module/" /etc/apache2/httpd.conf \
    && sed -i "s/#LoadModule\ session_module/LoadModule\ session_module/" /etc/apache2/httpd.conf \
    && sed -i "s/#LoadModule\ session_cookie_module/LoadModule\ session_cookie_module/" /etc/apache2/httpd.conf \
    && sed -i "s/#LoadModule\ session_crypto_module/LoadModule\ session_crypto_module/" /etc/apache2/httpd.conf \
    && sed -i "s/#LoadModule\ deflate_module/LoadModule\ deflate_module/" /etc/apache2/httpd.conf \
    && sed -i "s#^DocumentRoot \".*#DocumentRoot \"/var/www/html\"#g" /etc/apache2/httpd.conf \
    && sed -i "s#/var/www/localhost/htdocs#/var/www/html#" /etc/apache2/httpd.conf \
    && printf "\n<Directory \"/var/www/html\">\n\tAllowOverride All\n</Directory>\n" >> /etc/apache2/httpd.conf

RUN set -ex; \
    apk add --no-cache --virtual .fetch-deps \
    gnupg \
    ; \
    curl -o /usr/local/bin/wp.gpg -fSL "https://github.com/wp-cli/wp-cli/releases/download/v${WORDPRESS_CLI_VERSION}/wp-cli-${WORDPRESS_CLI_VERSION}.phar.gpg"; \
    export GNUPGHOME="$(mktemp -d)"; \
    gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys "$WORDPRESS_CLI_GPG_KEY"; \
    gpg --batch --decrypt --output /usr/local/bin/wp /usr/local/bin/wp.gpg; \
    command -v gpgconf && gpgconf --kill all || :; \
    rm -rf "$GNUPGHOME" /usr/local/bin/wp.gpg; \
    echo "$WORDPRESS_CLI_SHA512 */usr/local/bin/wp" | sha512sum -c -; \
    chmod +x /usr/local/bin/wp; \
    apk del .fetch-deps; \
    wp --allow-root --version

RUN cp /usr/bin/php7 /usr/bin/php && rm -f /var/cache/apk/*
RUN wp core download --allow-root --path=/var/www/html --locale=${WORDPRESS_LANG}

ADD run.sh /root
RUN chmod +x /root/run.sh

HEALTHCHECK CMD curl --fail http://localhost || exit 1
EXPOSE 80 443
ENTRYPOINT ["/root/run.sh"]