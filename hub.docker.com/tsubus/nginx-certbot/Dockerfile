FROM tsubus/archlinux
MAINTAINER tsubus

ARG VERSION="1.1"
LABEL build_version="nginx-certbot version:- ${VERSION}"
LABEL maintainer="tsubus"

RUN \
    echo "**** install packages ****" && \
    pacman -Syu --noconfirm && \
    pacman -S --noconfirm \
    nginx-mainline \
    certbot \
    certbot-nginx \
    php-fpm \
    cronie \
    grep \
    phpmyadmin \
    mariadb \
    procps && \
    echo "**** add certbot to cron ****" && \
    echo "0 0,12 * * * root python -c 'import random; import time; time.sleep(random.random() * 3600)' && certbot renew" | tee -a /etc/crontab > /dev/null && \
    echo "**** fix php ****" && \
    sed -i "s#user = http.*#user = abc#g" /etc/php/php-fpm.d/www.conf && \
    sed -i "s#group = http.*#group = abc#g" /etc/php/php-fpm.d/www.conf && \
    sed -i "s#listen.owner =.*#listen.owner = abc#g" /etc/php/php-fpm.d/www.conf && \
    sed -i "s#listen.group =.*#listen.group = abc#g" /etc/php/php-fpm.d/www.conf && \
    sed -i "s#listen.acl_users =.*#listen.acl_users = abc#g" /etc/php/php-fpm.d/www.conf && \
    sed -i "s#listen.acl_groups =.*#listen.acl_groups = abc#g" /etc/php/php-fpm.d/www.conf && \
    sed -i "s#error_log = syslog.*#error_log = /config/log/php/error.log#g" /etc/php/php-fpm.conf && \
    sed -i "s#;extension=mysqli.*#extension=mysqli#g" /etc/php/php.ini && \
    echo "**** create PMA temp dir ****" && \
    mkdir /usr/share/webapps/phpMyAdmin/tmp && \
    chown abc:abc /usr/share/webapps/phpMyAdmin/tmp

# add local files
COPY root/ /

# set permissions of new executables and clean-up
RUN \
    chmod +x /bin/mysqlrootpasswd.sh /bin/certbotcheck.sh && \
    pacman -Scc --noconfirm && \
    rm -rf \
        /tmp/* \
        /var/tmp/*
