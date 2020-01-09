FROM ubuntu

LABEL maintainer="Rodrigo Cantarino <rodrigopcantarino@gmail.com>"

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y \
    # Apache
    apache2 \
    # PHP
    php \
    php-common \
    php-cli \
    # Optional System Utilities and Libraries
    libapache2-mod-php \
    php-xdebug \
    phpunit \
    # Optional Data Management Utilities and Libraries
    php-apcu \
    php-json \
    php-mysql \
    php-odbc \
    php-pgsql \
    php-sqlite3 \
    # Optional Graphics Utilities and Libraries
    php-gd \
    php-imagick \
    # Optional Web Utilities
    php-curl \
    php-ldap \
    php-soap \
    php-xml \
    # Other Utilities
    php-bz2 \
    php-mbstring \
    php-pclzip \
    php-zip \
    curl \
    nano \
    libpng-dev \
    libjpeg-dev \
    zip \
    unzip \
&& apt-get clean && apt-get autoclean && apt-get autoremove \
&& rm -rf /var/lib/apt/lists/*

# Setting environment vars
ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

# Enables apache rewrite module
RUN a2enmod rewrite
RUN /usr/sbin/a2ensite default-ssl
RUN /usr/sbin/a2enmod ssl

# Setting permissions so that apcu can create cache directories
RUN chmod -R 775 /var/www/html

# Label the server
LABEL Description="PHP 7 Webserver"

VOLUME /var/www/html

# If just want to test an application already installed in dockerhost
## Use ADD or COPY to copy dockerhost content (files, directory) into the container directory.
## In this case, it will copy all content from this context into the container /var/www/html/ directory.
## It's usefull to create images that will just test an application!
## The Dockerfile and 000-default.conf file (app virtualhost configuration)
##     must be inside the app root folder before running docker build image command.
# Copy virtualhost file
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

# Install composer
WORKDIR /usr/local/bin/
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod +x composer.phar
RUN mv composer.phar composer
RUN composer self-update

# Set path bin 
WORKDIR /root
RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc

WORKDIR /var/www/html
COPY apache2-foreground.sh /scripts/
RUN chmod +x /scripts/*

CMD ["/scripts/apache2-foreground.sh"]

EXPOSE 80 