FROM ubuntu:16.04

# 기본 모듈 설치
RUN apt-get update -y && apt-get upgrade -y && apt-get clean \
    && apt-get install -y vim cron curl software-properties-common smbclient unzip wget net-tools telnetd iputils-ping telnet
    
# PHP Repository 추가
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt-get update \
    # Apache2 및 PHP 7.2 모듈 설치
    && apt-get install -y --allow-unauthenticated openssl libapache2-mod-php7.2 php-imagick php7.2-common php7.2-curl php7.2-gd php7.2-imap php7.2-intl php7.2-json php7.2-ldap php7.2-mbstring php7.2-mysql php7.2-pgsql php-smbclient php-ssh2 php7.2-sqlite3 php7.2-xml php7.2-zip \
    # PHP Memory Cache 모듈 설치
    && apt-get install -y --allow-unauthenticated php-apcu php-redis

# ownCloud 다운로드 및 압축해제
RUN set -eux; \
    mkdir var/www/owncloud; \
    wget "https://download.owncloud.org/community/owncloud-10.2.0.zip"; \
    unzip owncloud-*.zip; \
    cp -r owncloud /var/www/; \
    chown -R www-data:www-data /var/www/owncloud/; \
    rm -r owncloud owncloud-*.zip

# ownCloud Config 설정
RUN touch /etc/apache2/sites-available/owncloud.conf

RUN { \
        echo 'Alias /owncloud "/var/www/owncloud/"'; \
        echo ''; \
        echo '<Directory /var/www/owncloud/>'; \
        echo 'Options +FollowSymlinks'; \
        echo 'AllowOverride All'; \
        echo ''; \
        echo '<IfModule mod_dav.c>'; \
        echo 'Dav off'; \
        echo '</IfModule>'; \
        echo ''; \
        echo 'SetEnv HOME /var/www/owncloud'; \
        echo 'SetEnv HTTP_HOME /var/www/owncloud'; \
        echo '</Directory>'; \
    } > /etc/apache2/sites-available/owncloud.conf

RUN ln -s /etc/apache2/sites-available/owncloud.conf /etc/apache2/sites-enabled/owncloud.conf

RUN set -eux ; \
    service apache2 stop; \
    a2enmod rewrite; \
    a2enmod headers; \
    a2enmod env; \
    a2enmod dir; \
    a2enmod mime; \
    a2enmod unique_id; \
    service apache2 start;

#Expose ports
EXPOSE 8080

# 서비스 시작
CMD apachectl -D FOREGROUND
#CMD ["service", "apache2", "start"]