FROM atlassian/bamboo-server:6.8
WORKDIR /bamboo

USER root

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

RUN  apt-get update \
    && apt-get install  -y \
    apt-transport-https \
    ca-certificates \
    curl make unzip wget git \
    ca-certificates unzip zip gzip tar \
    gnupg-agent \
    software-properties-common \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Node Repo
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

# Yarn Repo
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ rc main" | tee /etc/apt/sources.list.d/yarn.list

# Docker Repo
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg |  apt-key add - \
    && add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable"

# PHP Repo
RUN apt-get update \
    && apt-get install -y --no-install-recommends gnupg \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu bionic main" > /etc/apt/sources.list.d/ondrej-php.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install selected extensions and other stuff - blackfire-php
RUN apt-get update \
    && apt-get -y --no-install-recommends install php-pear php7.2-dev php-memcached \
    php7.2-mysql php7.2-pdo php7.2-sqlite php-redis php-xdebug php7.2-bcmath \
    php7.2-bz2 php7.2-gd php7.2-gmp php-imagick php7.2-imap php7.2-intl \
    php7.2-pspell php7.2-soap php-ssh2 php-yaml \
    php7.2-cli php7.2-curl php-apcu php-apcu-bc \
    php7.2-json php7.2-mbstring php7.2-opcache php7.2-readline php7.2-xml \
    php7.2-zip php7.2-fpm php-memcached php7.2-mysql php7.2-pdo php7.2-sqlite \
    php-redis php-xdebug php7.2-bcmath php7.2-bz2 php7.2-gd \
    php7.2-gmp php-imagick php7.2-imap php7.2-intl php7.2-pspell \
    php7.2-soap php-ssh2 php-yaml php7.2-dom \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Frontend Node etc.
RUN apt-get update \
    && apt-get -y --no-install-recommends install nodejs yarn \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install Docker
RUN apt-get update \
    && apt-get install  -y docker docker-ce docker-ce-cli containerd.io \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install Docker-Compose
RUN curl -L https://github.com/docker/compose/releases/download/1.24.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

# Install PHP-Ast
RUN pecl install ast && printf "\nextension=ast.so\n" >> /etc/php/7.2/fpm/php.ini \ 
    && printf "\nextension=ast.so\n" >> /etc/php/7.2/cli/php.ini \
    && export PHAN_ALLOW_XDEBUG=1

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

USER bamboo

# Composer Dependencies
RUN composer global require hirak/prestissimo \
    && composer clear-cache