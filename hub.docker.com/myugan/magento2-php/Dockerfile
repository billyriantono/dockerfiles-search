FROM ubuntu:16.04
LABEL maintainer="myugan59@gmail.com"

ENV LANG=en_US.UTF-8 LANGUAGE=en_US.UTF-8 LC_ALL=en_US.UTF-8
ENV MAGE_DIR="/var/www/html/magento2" MAGE_DATA="/var/www/html/data" MAGE_VER="2.3" 
ENV BASE_URL="http://magento.local" BASE_URL_SECURE="https://magento.local" FRONTNAME="admin" LANG="en_US" TZ="Asia/Jakarta" CURRENCY="USD"
ENV DB_HOST="mariadb" DB_NAME="magentodb" DB_USER="appuser" DB_PASS="appuser"
ENV ADMIN_FIRSTNAME="Magento" ADMIN_LASTNAME="Admin" ADMIN_EMAIL="admin@$BASE_URL" ADMIN_USER="appuser" ADMIN_PASS="appuser123"
ENV CACHE="redis"

# general
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install software-properties-common python-software-properties sudo git curl nano wget net-tools locales zip unzip htop screen gettext-base
RUN locale-gen en_US.UTF-8

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get install -y tzdata
RUN dpkg-reconfigure --frontend noninteractive tzdata 

# add php ppa
RUN add-apt-repository -y ppa:ondrej/php && apt-get update
RUN apt-get install -y php7.1 \
    php7.1-cli \
    php7.1-fpm \
    php7.1-common \
    php7.1-dev \
    php7.1-bcmath \
    php7.1-curl \
    php7.1-gd \
    php7.1-intl \    
    php7.1-mbstring \
    php7.1-opcache \
    php7.1-mysql \
    php7.1-imap \
    php7.1-simplexml \
    php7.1-soap \
    php7.1-xsl \
    php7.1-mcrypt \
    php7.1-zip \
    php7.1-json \
    php7.1-iconv \
    php7.1-xmlrpc 

# php config
RUN rm -f /etc/php/7.1/fpm/pool.d/www.conf
ADD etc/php/7.1/fpm/pool.d/appuser.conf /etc/php/7.1/fpm/pool.d/appuser.conf
ADD etc/php/7.1/fpm/php-fpm.conf /etc/php/7.1/fpm/php-fpm.conf
ADD etc/php/7.1/fpm/php.ini /etc/php/7.1/fpm/php.ini
ADD ioncube/ioncube_loader_lin_7.1.so /usr/lib/php/20160303/

# composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# create docker group and user
RUN groupadd -r -g 1002 appuser
RUN useradd -rm -d /home/appuser -s /bin/bash -G sudo -u 1002 -g 1002 appuser
ADD etc/sudoers /etc/sudoers
RUN mkdir -p /run/php
RUN chown -R appuser:appuser /var/lib/php /run/php /opt

# add .env and magectl
ADD .env /home/appuser/.env
RUN chown -R appuser:appuser /home/appuser/.env
ADD magectl /usr/sbin/magectl

# add entrypoint
ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

USER appuser
WORKDIR /home/appuser

EXPOSE 9000
ENTRYPOINT [ "/bin/bash" , "/entrypoint.sh"]