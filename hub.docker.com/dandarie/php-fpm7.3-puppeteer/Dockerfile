FROM phpdockerio/php73-fpm

ENV DEBIAN_FRONTEND noninteractive

COPY install_npm.sh /install_npm.sh

RUN apt-get update && apt-get -y upgrade \
    && apt-get -y --no-install-recommends install apt-utils mysql-client \
    dialog mc nano telnet php7.3-mysql php7.3-redis php7.3-gd php7.3-bcmath php7.3-bz2 \
    php7.3-geoip php7.3-intl php7.3-mbstring php7.3-tidy php7.3-soap php7.3-imagick php7.3-zip \
    libfontconfig ttf-mscorefonts-installer iputils-ping nano less \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* \
    && chmod +x /install_npm.sh && /install_npm.sh


WORKDIR "/var/www/php"
