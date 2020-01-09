FROM laravelshipyard/app:latest

USER root

# Install utilities
RUN apk add --no-cache \
        bash \
        coreutils \
        curl \
        git \
        mariadb-client \
        openssl \
        openssh \
        postgresql-client \
        redis \
        sqlite \
        subversion \
        tini \
        unzip \
        zip

# Disable Xdebug
RUN sed -i '/zend_extension/s/^/;/g' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Install Composer globally
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /tmp
RUN EXPECTED_SIGNATURE="$(wget -q -O - https://composer.github.io/installer.sig)" \
    && curl --silent --fail --location --retry 3 --output /tmp/installer.php --url https://getcomposer.org/installer \
    && ACTUAL_SIGNATURE="$(sha384sum /tmp/installer.php | cut -d " " -f 1)" \
    && if [[ ${EXPECTED_SIGNATURE} != ${ACTUAL_SIGNATURE} ]]; then \
           >&2 echo 'ERROR: Invalid installer signature. Aborting.' && exit 1; \
       fi \
    && php /tmp/installer.php --quiet --no-ansi --install-dir=/usr/bin --filename=composer \
    && rm /tmp/installer.php \
    && composer --ansi --version --no-interaction

# Add the super-duper fast composer installer
RUN composer global require hirak/prestissimo

# Add Laravel Envoy
RUN composer global require laravel/envoy

COPY --from=node:alpine /opt /opt
COPY --from=node:alpine /usr/local /usr/local

# Add Vue-cli
RUN yarn global add @vue/cli

USER www-data

ENTRYPOINT ["/sbin/tini", "--"]

CMD ["bash"]