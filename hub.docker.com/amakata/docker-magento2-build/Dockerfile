FROM ubuntu:18.04
LABEL maintainer "Yoshihisa AMAKATA <amakata@banyanpartners.co.jp>"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y software-properties-common \
    && apt-get install -y locales apt-utils debconf-utils && rm -rf /var/lib/apt/lists/* \
    && LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/apache2 \
    && LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y php7.1 php7.1-mcrypt php7.1-curl php7.1-bcmath php7.1-intl php7.1-xsl php7.1-soap php7.1-gd php7.1-mbstring php7.1-json php7.1-xml php7.1-zip php7.1-gettext php7.1-pdo-mysql php7.1-phpdbg php-xdebug \
    && phpenmod mcrypt　\
    && phpenmod curl \
    && echo "postfix postfix/mailname string your.hostname.com" | debconf-set-selections \
    && echo "postfix postfix/main_mailer_type string 'Internet Site'" | debconf-set-selections \
    && apt-get install -y mysql-client \
    && apt-get install -y unzip \
    && apt-get install -y mailutils \
    && apt-get install -y python \
    && apt-get install -y curl \
    && apt-get install -y git \
    && apt-get install -y jq \
    && apt-get install -y gosu \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN curl -sS https://files.magerun.net/n98-magerun.phar > /usr/local/bin/n98-magerun.phar && chmod 755 /usr/local/bin/n98-magerun.phar
RUN curl -sS http://gordalina.github.io/cachetool/downloads/cachetool.phar > /usr/local/bin/cachetool.phar && chmod 755 /usr/local/bin/cachetool.phar
RUN mkdir -p /var/www/magento
RUN mkdir -p /var/www/.ssh && chown www-data.www-data /var/www/.ssh
RUN mkdir -p /var/www/.composer && chown www-data.www-data /var/www/.composer
WORKDIR /var/www/magento

CMD ["/bin/bash", '--login']
