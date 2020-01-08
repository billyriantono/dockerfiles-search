FROM rammstein4o/base-image:0.4.0

ARG PHP_VERSION=7.1

LABEL maintainer="rado.salov@gmail.com" \
    version="${PHP_VERSION}" \
    description="PHP ${PHP_VERSION} image"

ENV PHP_VERSION ${PHP_VERSION}

USER root

RUN apt-get update -y && apt-get install --allow-unauthenticated -y software-properties-common && LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php \
    && apt-get update --allow-unauthenticated -y && apt-get upgrade --allow-unauthenticated -y \
    && apt-get install --no-install-recommends --no-install-suggests --allow-unauthenticated -y \
        php${PHP_VERSION}-mysql \
        php${PHP_VERSION}-curl \
        php${PHP_VERSION}-gd \
        php${PHP_VERSION}-xmlrpc \
        php${PHP_VERSION}-xsl \
        php${PHP_VERSION}-zip \
        php${PHP_VERSION}-bz2 \
        php${PHP_VERSION}-gmp \
        php${PHP_VERSION}-mbstring \
        php${PHP_VERSION}-tidy \
        php${PHP_VERSION}-fpm \
    && apt-get clean && apt -y autoremove \
    && echo "" >> /etc/supervisord.conf \
    && echo "[program:php-fpm]" >> /etc/supervisord.conf \
    && echo "command = /usr/sbin/php-fpm${PHP_VERSION} -c /etc/php/${PHP_VERSION}/fpm/php.ini -F" >> /etc/supervisord.conf \
    && echo "autostart=true" >> /etc/supervisord.conf \
    && echo "autorestart=true" >> /etc/supervisord.conf \
    && echo "priority=5" >> /etc/supervisord.conf \
    && echo "stdout_logfile=/dev/stdout" >> /etc/supervisord.conf \
    && echo "stdout_logfile_maxbytes=0" >> /etc/supervisord.conf \
    && echo "stderr_logfile=/dev/stderr" >> /etc/supervisord.conf \
    && echo "stderr_logfile_maxbytes=0" >> /etc/supervisord.conf

EXPOSE 9000

USER ${USERNAME}
