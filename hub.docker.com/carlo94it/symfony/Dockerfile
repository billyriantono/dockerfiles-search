FROM ubuntu:18.04
MAINTAINER Carlo Cassano <info@carloweb.it>
EXPOSE 80 443
VOLUME ["/srv/symfony"]

ENV DEBIAN_FRONTEND noninteractive

# Update packages
RUN apt-get update

# Install PHP PPA for PHP
RUN apt-get install -my software-properties-common && \
  add-apt-repository -my ppa:ondrej/php && \
  apt-get update

# Install packages
RUN apt-get install -my curl \
    wget \
    php7.3-curl \
    php7.3-gd \
    php7.3-xsl \
    php7.3-mysqlnd \
    php7.3-cli \
    php7.3-intl \
    php7.3-bz2 \
    php7.3-zip \
    php7.3-mbstring \
    php7.3-dev \
    php-pear \
    php7.3-imagick \
    php7.3-soap \
    php7.3-mysql \
    php7.3-sqlite3 \
    libmcrypt-dev \
    libcap2-bin \
    git \
    zip && \
  rm -rf /var/lib/apt/lists/*

# Install mcrypt with PECL
RUN pecl channel-update pecl.php.net && \
  yes '' | pecl install -f mcrypt-1.0.1 && \
  pecl clear-cache && \
  rm -rf /tmp/pear

# Download Composer
RUN cd /tmp && \
  php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php composer-setup.php && \
  php -r "unlink('composer-setup.php');" && \
  mv composer.phar /usr/bin/composer

# Download Symfony CLI
RUN wget https://get.symfony.com/cli/installer -O - | bash && mv /root/.symfony/bin/symfony /usr/local/bin/symfony

# Set permissions for non root users
RUN chmod 777 /srv/symfony && \
  setcap CAP_NET_BIND_SERVICE=+eip /usr/local/bin/symfony

COPY entrypoint.sh /srv/entrypoint.sh

WORKDIR /srv/symfony

ENTRYPOINT /srv/entrypoint.sh
