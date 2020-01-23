FROM roundcube/roundcubemail

RUN set -ex && \
    apt-get update && \
    apt-get install -y --no-install-recommends git && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
    mv /usr/src/roundcubemail/composer.json-dist /usr/src/roundcubemail/composer.json && \
    chown -R www-data:www-data /var/www /usr/src/roundcubemail

USER www-data

RUN composer \
        --working-dir=/usr/src/roundcubemail/ \
        --prefer-dist --prefer-stable \
        --no-update --no-interaction \
        --optimize-autoloader --apcu-autoloader \
        require \
            roundcube/plugin-installer \
            roundcube/carddav \
            johndoh/contextmenu

USER root

ENV ROUNDCUBEMAIL_PLUGINS plugin-installer,carddav,contextmenu,archive,zipdownload
