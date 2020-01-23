FROM phusion/baseimage:latest
MAINTAINER Allan Sun <allan.sun@bricre.com>

RUN     apt-get -y install --no-install-recommends software-properties-common && \
        locale-gen en_US.UTF-8 && export LANG=en_US.UTF-8 && export LC_ALL=en_US.UTF-8 && \
        apt-add-repository ppa:ondrej/php && \
        apt-add-repository ppa:ondrej/pkg-gearman && \
        curl -s https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
        sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >>/etc/apt/sources.list.d/google.list' && \
        apt-get update && \

        # Install necessary packagies
        apt-get -yq install --no-install-recommends \
        iputils-ping \
        php7.0-cli php7.0-calendar php7.0-ctype php7.0-fileinfo php7.0-ftp php7.0-gettext php7.0-pdo \
        php7.0-redis php7.0-gd php7.0-curl php7.0-intl php7.0-soap php7.0-iconv php7.0-readline php7.0-mysql \
        php7.0-json php7.0-mcrypt php7.0-opcache php7.0-xml php7.0-zip php7.0-redis php7.0-gearman php-pear zlib1g-dev \
        php7.0-dev php7.0-imagick php7.0-fpm php7.0-phalcon ghostscript php-ssh2 make google-chrome-stable dmtx-utils && \
        pecl install grpc-1.3.2 && \
        pecl install mongodb && \
        echo "extension=mongodb.so" >> /etc/php/7.0/cli/conf.d/20-mongodb.ini && \
        echo "extension=mongodb.so" >> /etc/php/7.0/fpm/conf.d/20-mongodb.ini && \
        apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV     APP_ENVIRONMENT=development
EXPOSE 9000
RUN     mkdir -p /run/php

CMD ["php-fpm7.0","-F"] 

# Add configs
RUN     rm -rf /etc/service/cron /etc/service/sshd
