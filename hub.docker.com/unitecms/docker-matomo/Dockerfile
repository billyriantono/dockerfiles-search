#
# Matomo Docker Image
#

FROM unitecms/docker-nginx-php-fpm

ENV MATOMO_VERSION 3.5.1

ENV NAME=matomo \
    SUMMARY="matomo image" \
    DESCRIPTION="matomo image" \
    APP_ROOT=/app \
    PATH=/app/bin:$PATH

LABEL summary="${SUMMARY}" \
      description="${DESCRIPTION}" \
      io.k8s.description="${DESCRIPTION}" \
      io.k8s.display-name="${DESCRIPTION}" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="${NAME}" \
      name="unitecms/docker-matomo" \
      version="1" \
      maintainer="www.unitecms.io <stefan@unite.co.at>"

USER root

COPY ./root/ /

RUN fix-permissions /etc/nginx

RUN mkdir /app

WORKDIR ${APP_ROOT}

RUN rpm-file-permissions && \
    useradd -u 1001 -r -g 0 -d ${APP_ROOT} -s /sbin/nologin \
      -c "Default Application User" default && \
    chown -R 1001:0 ${APP_ROOT}

RUN wget http://builds.piwik.org/matomo-latest.zip
RUN unzip matomo-latest.zip
RUN rm matomo-latest.zip

RUN yum install -y php72-php-pecl-geoip
RUN echo "geoip.custom_directory=/app/matomo/misc" >> /etc/php.d/geoip.ini

RUN sed -i 's/php_admin_value\[disable_functions\].*/php_admin_value[disable_functions] = system, show_source, symlink, exec, dl, passthru, escapeshellarg, escapeshellcmd/' /etc/php-fpm.d/www.conf

#ADD test/index.php /app/matomo/index.php

RUN chown -R 1001:0 ${APP_ROOT}

USER 1001
VOLUME /app