FROM ubuntu:xenial
EXPOSE 80

RUN apt-get update

# Install base packages
RUN apt-get -y install software-properties-common python-software-properties
RUN apt-get -y install curl zip unzip tree git openssh-client fakeroot

# Install PHP 7.2
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN apt-get update
RUN apt-get -y install php7.2 php7.2-cli php7.2-common php7.2-curl php7.2-gd php7.2-json php7.2-mbstring php7.2-intl php7.2-mysql php7.2-sqlite3 php7.2-xml php7.2-zip
RUN apt-get -y install php-xdebug

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

# Install apache 2
RUN apt-get -y install apache2
# Enable apache modules
RUN a2enmod php7.2
RUN a2enmod rewrite

# Install node
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get -y install nodejs

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update
RUN apt-get -y install yarn

# Install supervisor
RUN apt-get -y install supervisor && mkdir -p /var/log/supervisor && mkdir -p /etc/supervisor/conf.d
COPY etc/supervisor/supervisord.conf /etc/supervisor/supervisord.conf
COPY etc/supervisor/conf.d/apache2.conf /etc/supervisor/conf.d/apache2.conf
CMD supervisord -c /etc/supervisor/supervisord.conf
