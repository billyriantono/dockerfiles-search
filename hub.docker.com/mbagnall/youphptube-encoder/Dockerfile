# Probo Ubuntu PHP Image
#
# This script builds the PHP containers for ProboCI. It is built off a foundation of tools built in
# mbagnall/probo-lamp:ubuntu-base

# Base this off Ubuntu 18.04
FROM ubuntu:18.04

LABEL name="ProboCI PHP Image"
LABEL description="Unified ProboCI Image. All versions of PHP available via yaml configuration."
LABEL author="Michael R. Bagnall <mrbagnall@icloud.com>"
LABEL vendor="ProboCI, LLC."

WORKDIR /root

ENV TERM xterm

# Add ondrej/php PPA repository for PHP.
RUN apt update -y
RUN DEBIAN_FRONTEND=noninteractive && \
  apt-get install -y tzdata && \
  ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime && \
  dpkg-reconfigure --frontend noninteractive tzdata

RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php && \
  add-apt-repository ppa:jonathonf/ffmpeg-4 && \
  apt update -y && \
  apt-get install -y \
    git \
    libmcrypt-dev \
    php7.2 \
    php7.2-bcmath \
    php7.2-bz2 \
    php7.2-cli \
    php7.2-common \
    php7.2-curl \
    php7.2-dba \
    php7.2-gd \
    php7.2-json \
    php7.2-ldap \
    php7.2-mbstring \
    php7.2-mysql \
    php7.2-opcache \
    php7.2-readline \
    php7.2-soap \
    php7.2-zip \
    php7.2-pgsql \
    php7.2-dev \
    php7.2-xml \
    libapache2-mod-php7.2 \
    php-imagick \
    php-pear \
    youtube-dl \
    libimage-exiftool-perl \
    ffmpeg && \
  pecl channel-update pecl.php.net && \
  pecl install mcrypt-1.0.2 && \
  rm -rf /var/www/html \
    && a2enmod rewrite \
    && a2enmod actions \
    && a2enmod alias \
    && a2enmod deflate \
    && a2enmod dir \
    && a2enmod expires \
    && a2enmod headers \
    && a2enmod mime \
    && a2enmod negotiation \
    && a2enmod setenvif \
    && a2enmod proxy \
    && a2enmod proxy_http \
    && a2enmod speling

RUN mkdir -p /var/www/html && \
  cd /var/www/html && \
  git clone https://github.com/YouPHPTube/YouPHPTube-Encoder.git encoder && \
  chown -R www-data:www-data /var/www/html

COPY etc/php.ini /etc/php.ini
COPY etc/apache2/apache2.conf /etc/apache2/apache2-noauth.conf

ADD conf/run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh
RUN chown www-data:www-data /run-httpd.sh

VOLUME ["/var/www"]

EXPOSE 80 443

CMD ["/run-httpd.sh"]

