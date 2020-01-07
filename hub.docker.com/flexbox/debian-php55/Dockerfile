FROM debian:wheezy

LABEL maintainer="Alex Karshin <https://flexbox.it>"
LABEL source="https://bitbucket.org/flexboxIT/debian-php55"

RUN usermod -u 1000 www-data
RUN groupmod -g 1000 www-data

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E9C74FEEA2098A6E && \
    echo "deb http://packages.dotdeb.org/ wheezy-php55 all" > /etc/apt/sources.list.d/php.list && \
    echo "deb http://ftp.debian.org/debian wheezy-backports main contrib non-free" >> /etc/apt/sources.list.d/php.list

RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y \
        build-essential \
        curl \
        php5-cli \
        php5-xdebug \
        php5-imagick \
        php5-gd \
        php5-mongo \
        php5-curl \
        php5-mcrypt \
        php5-intl \
        php5-mysql \
        php5-sqlite \
        php5-redis \
        php5-pgsql \
        nano \
        git \
        postfix \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y php5-fpm \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y nginx

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs \
    && /usr/bin/npm install -g gulp \
    && /usr/bin/npm install -g bower

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

COPY start.sh /tmp/start.sh
COPY php/memory.ini /usr/local/etc/php/conf.d/memory.ini
COPY php/datetime.ini /etc/php5/fpm/conf.d/01-datetime.ini
COPY php/datetime.ini /etc/php5/cli/conf.d/01-datetime.ini
COPY postfix/main.cf /etc/postfix/main.cf

WORKDIR /html

EXPOSE 80 443

CMD ["/tmp/start.sh"]
