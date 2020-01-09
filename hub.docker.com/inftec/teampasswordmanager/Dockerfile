FROM php:7.2-apache
MAINTAINER Fabian Gut <fabian.gut@inftec.ch>, InfTec GmbH

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

RUN apt-get update && \
    apt-get install -y \
        gosu \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libldap2-dev \
        libmcrypt-dev \
        libpng-dev \
        unzip && \
    apt-get autoclean

RUN docker-php-ext-install -j$(nproc) \
        gd \
        ldap \
        mysqli

RUN rm /etc/timezone && \
    rm /etc/localtime && \
    echo PURGE | debconf-communicate -f noninteractive tzdata && \
    echo "tzdata tzdata/Zones/Europe select Zurich" | debconf-set-selections && \
    echo "tzdata tzdata/Areas select Europe" | debconf-set-selections && \
    debconf-show tzdata && \
    dpkg-reconfigure -f noninteractive tzdata

RUN echo "session.gc_maxlifetime = 32400" >> $PHP_INI_DIR/conf.d/tpm.ini

ENV PHP_EXTENSIONS_LIB_DIR /usr/local/lib/php/extensions/no-debug-non-zts-20170718
ENV IONCUBE_LOADER_PHP_VERSION 7.2
ENV IONCUBE_LOADER_VERSION 10.3.2

RUN curl -Lks https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz -o ioncube.tar.gz && \
    tar xzf ioncube.tar.gz && \
    mv ioncube/ioncube_loader_lin_${IONCUBE_LOADER_PHP_VERSION}* ${PHP_EXTENSIONS_LIB_DIR}/ && \
    chmod 644 ${PHP_EXTENSIONS_LIB_DIR}/ioncube_loader_lin_${IONCUBE_LOADER_PHP_VERSION}* && \
    rm -rf ioncube ioncube.tar.gz && \
    echo "zend_extension = ${PHP_EXTENSIONS_LIB_DIR}/ioncube_loader_lin_${IONCUBE_LOADER_PHP_VERSION}.so" >> $PHP_INI_DIR/conf.d/00-ioncube.ini

ENV TEAM_PASSWORD_MANAGER_VERSION 7.84.198

RUN curl -Lks https://teampasswordmanager.com/assets/download/teampasswordmanager_${TEAM_PASSWORD_MANAGER_VERSION}.zip -o teampasswordmanager.zip && \
    unzip teampasswordmanager.zip && \
    cp -r teampasswordmanager_${TEAM_PASSWORD_MANAGER_VERSION}/* . && \
    rm -rf teampasswordmanager_${TEAM_PASSWORD_MANAGER_VERSION} teampasswordmanager.zip install.txt eula.txt upgrade.txt
 
COPY assets/tpm.init /opt/tpm-setup/tpm.init
COPY assets/config/config.php /opt/tpm-setup/config/config.php
RUN chmod 766 /opt/tpm-setup/tpm.init
 
VOLUME /var/www/html/uploads
ENTRYPOINT ["/opt/tpm-setup/tpm.init"]
CMD ["tpm:start"]
