FROM debian:jessie

MAINTAINER "kairee <kaireewu@gmail.com>"

ARG DEBIAN_FRONTEND=noninteractive
ARG CN_MIRROR=0

ADD ./163.jessie ./

# Use 163 mirror for chinese users.
RUN if [ $CN_MIRROR  = 1  ]; then cp -f 163.jessie /etc/apt/sources.list; fi && apt update

# Create user "laravel"
RUN adduser --disabled-password --gecos "" laravel

# Install base packages
RUN apt-get update && apt-get --no-install-recommends install -y curl apt-utils apt-transport-https ca-certificates build-essential git unzip supervisor mysql-client openssh-client

# Install node 7.x
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - && apt-get update && apt-get --no-install-recommends install -y nodejs
# Install marked & node-gyp globally
RUN npm i -g marked node-gyp

# Add key and repository for php 7.1
RUN curl -sLo /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    echo "deb https://packages.sury.org/php/ jessie main" > /etc/apt/sources.list.d/php.list

RUN apt-get update && apt-get --no-install-recommends install -y php7.1-cli php7.1-curl php7.1-pdo php7.1-mysqlnd php7.1-mcrypt php7.1-mbstring php7.1-dom php7.1-xdebug php7.1-tidy php7.1-gd php7.1-zip php7.1-intl && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    mv composer.phar /usr/local/bin/composer && \
    php -r "unlink('composer-setup.php');"
