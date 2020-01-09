FROM webdevops/php-nginx-dev:7.2
MAINTAINER Nando Bosshart <nando@webstobe.ch>
# set ENV variables
ENV COMPOSER_ALLOW_SUPERUSER=1 PATH="/var/www/vendor/bin:$PATH"
ENV WEB_DOCUMENT_ROOT=/var/www/web \
    WEB_DOCUMENT_INDEX=index.php \
    WEB_ALIAS_DOMAIN=*.local \
    WEB_PHP_TIMEOUT=600 \
    WEB_PHP_SOCKET="" \
    PHP_MAX_EXECUTION_TIME=600 \
    PHP_DATE_TIMEZONE="Europe/Zurich"
ENV WEB_PHP_SOCKET=127.0.0.1:9000
ENV WEB_NO_CACHE_PATTERN="\.(css|js|gif|png|jpg|svg|json|xml)$"
# install some additions on top of our image
RUN apt update && \
    apt install -y --no-install-recommends \
        gifsicle \
        poppler-utils \
        mysql-client \
        && docker-image-cleanup
# add custom-entrypoint.sh
COPY entrypoint.sh /opt/docker/provision/entrypoint.d/
RUN chmod +x /opt/docker/provision/entrypoint.d/entrypoint.sh
