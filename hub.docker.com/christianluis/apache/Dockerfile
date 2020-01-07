FROM ubuntu:xenial

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update && \
    apt-get -y dist-upgrade && \
    apt-get install -y language-pack-en-base &&\
    export LC_ALL=en_US.UTF-8 && \
    export LANG=en_US.UTF-8

RUN locale-gen de_DE.UTF-8

RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install \
    software-properties-common nano curl lynx-cur wget ca-certificates git tzdata zip mysql-client

RUN ln -fs /usr/share/zoneinfo/Europe/Berlin /etc/localtime && dpkg-reconfigure -f noninteractive tzdata

RUN DEBIAN_FRONTEND=noninteractive LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php && \
    DEBIAN_FRONTEND=noninteractive LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/apache2

RUN DEBIAN_FRONTEND=noninteractive LC_ALL=en_US.UTF-8 \
    apt-get update && apt-get install -y \
    apache2  \
    libapache2-mod-php7.1 php7.1 php7.1-mysql php7.1-curl php7.1-gd php7.1-soap php7.1-xml php7.1-zip php-imagick php7.1-mcrypt php7.1-mysql php7.1-mbstring php7.1-intl php7.1-bcmath php-redis ghostscript graphicsmagick

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY ./config/php/php.ini /etc/php/7.1/apache2/
COPY ./config/php/php.ini /etc/php/7.1/cli/

RUN a2enmod rewrite && \
    a2enmod php7.1 && \
    a2enmod auth_basic && \
    a2enmod deflate && \
    a2enmod expires && \
    a2enmod headers && \
    a2enmod status && \
    a2enmod authz_user && \
    a2enmod authz_core && \
    a2enmod alias && \
    a2enmod authn_core && \
    a2enmod authn_file && \
    a2enmod reqtimeout && \
    a2enmod negotiation && \
    a2enmod autoindex && \
    a2enmod access_compat && \
    a2enmod vhost_alias && \
    a2enmod filter && \
    a2enmod ssl && \
    a2enmod env

COPY apache2-foreground /usr/local/bin/
RUN chmod +x /usr/local/bin/apache2-foreground

ADD ./config/apache/000-default.conf  /etc/apache2/sites-available/
ADD ./config/bash/.bashrc  /root/.bashrc

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

WORKDIR /var/www

EXPOSE 80

CMD ["bash", "/usr/local/bin/apache2-foreground"]