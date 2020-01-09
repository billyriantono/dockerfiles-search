#
# Nginx image PHP 7.2 / PHP FPM
#


FROM unitecms/docker-centos

ENV PHP_VERSION=7.2 \
    PHP_VER_SHORT=72 \
    NAME=nginx-php

ENV SUMMARY="Nginx 1.12 / PHP 7.2 FPM image" \
    DESCRIPTION="Nginx 1.12 / PHP 7.2 FPM image"

LABEL summary="${SUMMARY}" \
      description="${DESCRIPTION}" \
      io.k8s.description="${DESCRIPTION}" \
      io.k8s.display-name="${DESCRIPTION}" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="${DESCRIPTION}" \
      name="unitecms/docker-nginx-php-fpm" \
      version="1" \
      maintainer="www.unitecms.io <stefan@unite.co.at>"

# Install required repos, update, and then install PHP-FPM
RUN yum install -y epel-release \ 
        http://rpms.remirepo.net/enterprise/remi-release-7.rpm  \
        yum-utils && \
    yum-config-manager --enable remi-php72 && \
    yum install -y \
        php-bcmath \
        php-cli \
        php-fpm \
        php-mysqlnd \
        php-xml \
        php-intl \
        php-gd \
        php-mcrypt \
        php-mbstring \
        php-opcache \
        php-pdo

# install nginx / mysql client
RUN yum install -y yum-utils  && \
    INSTALL_PKGS="nginx mariadb" && \
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS

# Installing supervisor
RUN yum install -y python-setuptools
RUN easy_install pip
RUN pip install supervisor

# cleanup to reduce size
RUN yum clean all && \
    rm -rf /var/cache/yum

COPY ./root/ /

# set timezone php
RUN sed -i "s/;date.timezone =.*/date.timezone = Europe\/Vienna/" /etc/php.ini

RUN container-setup && rpm-file-permissions

USER 1001

# supervisord
ENTRYPOINT ["container-entrypoint"]
CMD ["supervisord", "-n"]
