FROM appsvcorg/nginx-fpm:0.2
MAINTAINER Azure App Service Container Images <appsvc-images@microsoft.com>

# ========
# ENV vars
# ========
#
ENV DOCKER_BUILD_HOME "/dockerbuild"
# drupal 
ENV DRUPAL_SOURCE "/usr/src/drupal" 
ENV DRUPAL_HOME "/home/site/wwwroot"
# mariadb
ENV MARIADB_DATA_DIR "/home/data/mysql"
ENV MARIADB_LOG_DIR "/home/LogFiles/mysql"
# phpmyadmin
ENV PHPMYADMIN_SOURCE "/usr/src/phpmyadmin"
ENV PHPMYADMIN_HOME "/home/phpmyadmin"
#nginx
ENV NGINX_LOG_DIR "/home/LogFiles/nginx"
#RUN { \
#      echo 'client_max_body_size 20M;'; \
#    } > /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/
#php
ENV PHP_HOME "/etc/php/7.0"
ENV PHP_CONF_DIR $PHP_HOME"/cli"
ENV PHP_CONF_FILE $PHP_CONF_DIR"/php.ini"

COPY php.ini /etc/php/7.0/fpm/

# Allow to include custom php-fpm config, e.g. to set environment variables
RUN echo 'include=/usr/local/etc/conf.d/*' >> /usr/local/etc/php-fpm.conf \
    && mkdir /usr/local/etc/conf.d/

COPY run-php-fpm /usr/local/bin/

CMD ["run-php-fpm"]

# ====================
# Download and Install
# ~. essentials
# 1. Drupal
# ====================

RUN mkdir -p $DOCKER_BUILD_HOME
WORKDIR $DOCKER_BUILD_HOME

# -------------
# 1. Drupal
# -------------
RUN  mkdir -p $DRUPAL_SOURCE 
COPY drupal.tar.gz $DRUPAL_SOURCE/

# =========
# Configure
# =========
WORKDIR $DRUPAL_HOME
RUN rm -rf $DOCKER_BUILD_HOME

COPY www.conf /etc/php/7.0/fpm/pool.d/

# =====
# final
# =====
COPY entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh

EXPOSE 2222 80
ENTRYPOINT ["entrypoint.sh"]
