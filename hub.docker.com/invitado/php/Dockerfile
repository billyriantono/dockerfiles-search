FROM php:7.3.11-fpm-alpine

# Install needed PHP extensions.
RUN apk add --update libpng-dev libjpeg-turbo-dev && rm -rf /var/cache/apk/*
RUN docker-php-ext-configure gd \
    --with-gd \
    --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install pdo_mysql sockets opcache bcmath gd

# Install MailParse package.
RUN apk add --update --no-cache $PHPIZE_DEPS \
    && pecl install mailparse-3.0.3 \
    && docker-php-ext-enable mailparse \
    && apk del $PHPIZE_DEPS

# Install AMQP extension.
RUN apk add --update --no-cache php7-pecl-amqp \
    && mv /usr/lib/php7/modules/amqp.so /usr/local/lib/php/extensions/no-debug-non-zts-20180731/amqp.so \
    && mv /etc/php7/conf.d/40_amqp.ini /usr/local/etc/php/conf.d/40_amqp.ini

# JAVA JRE
# Default to UTF-8 file.encoding.
ENV LANG en_US.UTF-8

# Add script to detect java path.
RUN { \
        echo '#!/bin/sh'; \
        echo 'set -e'; \
        echo; \
        echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
    } > /usr/local/bin/docker-java-home \
    && chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk/jre
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

# Install Java.
RUN set -x \
    && apk add --no-cache openjdk8-jre \
    && [ "$JAVA_HOME" = "$(docker-java-home)" ]

# Install some default fonts.
RUN apk add --update fontconfig ttf-dejavu \
    && rm -rf /var/cache/apk/*

# Add PD4ML.
COPY ./pd4ml/pd4ml.jar /opt/pd4ml.jar
RUN chmod +x /opt/pd4ml.jar

COPY ./pd4ml/ss_css2.jar /opt/ss_css2.jar
RUN chmod +x /opt/ss_css2.jar

COPY ./pd4ml/fonts.jar /opt/fonts.jar
RUN chmod +x /opt/fonts.jar

# Install S6.
RUN apk add --update --no-cache s6

# Add Opcache configuration files.
COPY ./opcache.ini /opt/opcache.ini

# Add other PHP configuration.
COPY ./other.ini /usr/local/etc/php/conf.d/other.ini

# Add PHP-FPM configuration files.
RUN rm -rf /usr/local/etc/php-fpm.d/*
COPY ./php-fpm.conf /usr/local/etc/php-fpm.d/php-fpm.conf

# Add entrypoint script.
COPY ./entrypoint.sh /opt/entrypoint.sh
RUN chmod 755 /opt/entrypoint.sh
CMD ["/opt/entrypoint.sh"]
