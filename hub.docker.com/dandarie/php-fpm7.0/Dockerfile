FROM phpdockerio/php7-fpm:latest

ENV DEBIAN_FRONTEND noninteractive

# Install selected extensions and other stuff
RUN apt-get update && apt-get -y upgrade \
    && apt-get -y --no-install-recommends install mysql-client libfontconfig \
    dialog mc telnet php7.0-mysql php7.0-redis php7.0-gd \
    php7.0-geoip php7.0-intl php7.0-mbstring php-tidy php-soap \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*


WORKDIR "/var/www/php"
