FROM debian:stretch

# update package repository and upgrade installed packages if available
RUN apt update && apt update
RUN apt install -y apt-transport-https ca-certificates wget curl

# ADD php to source and update package repository again
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
    && sh -c 'echo "deb https://packages.sury.org/php/ stretch main" > /etc/apt/sources.list.d/php.list' \
    && apt update


# Install php packages
RUN apt-get install -y \
        php7.3 \
        php7.3-common \
        php7.3-json \
        php7.3-mbstring \
        php7.3-apcu \
        php7.3-bcmath \
        php7.3-cli \
        php7.3-curl \
        php7.3-fpm \
        php7.3-gd \
        php7.3-intl \
        php7.3-mysql \
        php7.3-soap \
        php7.3-xml \
        php7.3-zip \
        php7.3-imagick

# INSTALL apache and enable some mods
RUN apt install -y apache2 \
    &&  a2enmod rewrite headers

# Set Apache User and Group
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2


CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
EXPOSE 80
EXPOSE 443