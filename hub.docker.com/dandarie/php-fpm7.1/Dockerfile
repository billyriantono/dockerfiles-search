FROM phpdockerio/php71-fpm

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y upgrade \
    && apt-get -y --no-install-recommends install apt-utils mysql-client \
    dialog mc telnet php7.1-mysql php7.1-redis php7.1-gd php7.1-bz2 \
    php7.1-geoip php7.1-intl php7.1-mbstring php7.1-tidy php7.1-soap php7.1-imagick \
    libfontconfig ttf-mscorefonts-installer nano less grep php7.1-bcmath unzip \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*


WORKDIR "/var/www/php"
