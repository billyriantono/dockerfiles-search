FROM php:fpm-alpine3.9

# Add the dependencies as a variable so we can use the same list to remove them.
# Not doing so will make the image bigger, something that we should avoid when
# downloading this from Docker Hub, or it will take ages to finally download.
ARG DEVPACKAGES="\
    bzip2-dev \
    freetype-dev \
    gettext-dev \
    graphicsmagick-dev \
    icu-dev \
    krb5-dev \
    imap-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libtirpc-dev \
    libtool \
    libxml2-dev \
    libzip-dev \
    openldap-dev \
    openssl-dev \
    postgresql-dev \
    rabbitmq-c-dev \
    sqlite-dev \
    tidyhtml-dev"

# Since Xdebug usually is a little behind PHP latest stable version, we will need 
# to put the version number otherwise we may download an incompatible version.
# Using an argument allows us to update Xdebug package via docker-compose.
ARG XDEBUGVERSION="2.7.0RC1"

# Here we will install the packages we need to compile PHP and some others, but
# we will add the shared libreries needed for some extensions to work. If we
# don't do this, the extensions will be registered but won't load in PHP.
RUN apk add --no-cache --virtual php-shared-libraries \
        c-client \
        graphicsmagick \
        icu-libs \
        imap \
        libbz2 \
        libpng \
        libintl \
        libldap \
        libpq \
        libzip \
        nghttp2 \
        rabbitmq-c \
        tidyhtml-libs \
        wkhtmltopdf

# Then we delete the APK packages we used to compile the extensions, while leaving
# the rest of shared libraries the extensions use. If there are packages in the
# APK cache, we will ensure to delete them so slim down the resulting image.

# We need to do this in only one RUN to keep the image from 400MB to 150MB or less.
# This happens beapk delcause the layers adds up themselves, they won't free up space
# even if you delete files from the last layer. Is kind of tricky, isn't?

# We need to install Redis with igbinay separated, since the install flag doesn't
# accept configuration options. We will use Docker's helpers for that matter
# while we first intall igbinary. Welp, PHPRedis depends on it. That is.
RUN apk --no-cache add $PHPIZE_DEPS $DEVPACKAGES \
    && pecl install igbinary \
    && docker-php-ext-enable igbinary \
    && pecl install --onlyreqdeps --nobuild redis \
    && docker-php-ext-configure "$(pecl config-get temp_dir)/redis" --enable-redis-igbinary \
    && docker-php-ext-install "$(pecl config-get temp_dir)/redis" \
    && pecl install \
           amqp \
           gmagick-2.0.5RC1 \
           xdebug-$XDEBUGVERSION  \
    && docker-php-ext-enable \
           amqp \
           gmagick \
           xdebug \
    && docker-php-ext-install \
           bcmath \
           bz2 \
           exif \
           gettext \
           intl \
           ldap \
           opcache \
           pcntl \
           pdo_mysql \
           pdo_pgsql \
           pdo_sqlite \
           posix \
           soap \
           sockets \
           tidy \
           xmlrpc \
           gd \
           imap \
           zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-configure imap --with-kerberos --with-imap --with-imap-ssl \
    && docker-php-ext-install imap \
    && apk del --no-cache $PHPIZE_DEPS $DEVPACKAGES \
    && rm -f /var/cache/apk/*  \
    && pear clear-cache

# Configure Xdebug
ENV XDEBUG_ENABLED=false
RUN echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_host=host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Configure igbinary as default serialization for Sessions
RUN echo "session.serialize_handler=igbinary" >> /usr/local/etc/php/conf.d/docker-php-ext-redis.ini \
    && echo "igbinary.compact_strings=On" >> /usr/local/etc/php/conf.d/docker-php-ext-redis.ini

COPY run.sh /run.sh

WORKDIR /var/www

CMD ["/run.sh"]