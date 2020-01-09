FROM php:7.1-apache-jessie

# set defaults or env vars for Elgg and MySQL
# Timezone
ENV TIMEZONE=${TIMEZONE:-"Europe/Madrid"}

# MySQL
ENV MYSQL_USER=${MYSQL_USER:-"root"}
ENV MYSQL_PASS=${MYSQL_PASS:-"root"}
ENV MYSQL_PORT=${MYSQL_PORT:-"3306"}

# required for installation
ENV ELGG_DB_HOST=${ELGG_DB_HOST:-"mysql"}
ENV ELGG_DB_USER=$MYSQL_USER
ENV ELGG_DB_PASS=$MYSQL_PASS
ENV ELGG_DB_NAME=${ELGG_DB_NAME:-"elgg"}

ENV ELGG_SITE_NAME=${ELGG_SITE_NAME:-"Elgg Site"}
ENV ELGG_DATA_ROOT=${ELGG_DATA_ROOT:-"/media/elgg/"}
ENV ELGG_WWW_ROOT=${ELGG_WWW_ROOT:-"http://localhost:8000"}

# admin user setup
ENV ELGG_DISPLAY_NAME=${ELGG_DISPLAY_NAME:-"Admin"}
ENV ELGG_EMAIL=${ELGG_EMAIL:-"admin@myelgg.org"}
ENV ELGG_USERNAME=${ELGG_USERNAME:-"admin"}
ENV ELGG_PASSWORD=${ELGG_PASSWORD:-"admin"}

# optional for installation
ENV ELGG_DB_PREFIX=${ELGG_DB_PREFIX:-"elgg_"}
ENV ELGG_PATH=${ELGG_PATH:-"/var/www/html/"}
# 2 is ACCESS_PUBLIC
ENV ELGG_SITE_ACCESS=${ELGG_SITE_ACCESS:-"2"}

# elgg version to download
ENV ELGG_VERSION=${ELGG_VERSION:-"2.3.3"}

COPY . /elgg-php7/
COPY docker_config/php.ini /usr/local/etc/php/

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        netcat \
        mysql-client \
        wget \
        git \
        unzip

# Install composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    printf "\nPATH=\"~/.composer/vendor/bin:\$PATH\"\n" | tee -a ~/.bashrc

# Elgg requirements
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install pdo pdo_mysql mysqli
RUN docker-php-ext-install mbstring

WORKDIR ${ELGG_PATH}

#Configs apache
RUN a2enmod rewrite

#Set time zone
RUN cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime
RUN sed -i "s#{{timezone}}#$TIMEZONE#g" /usr/local/etc/php/php.ini

# Create base directory
RUN mkdir /elgg-src

# Elgg installation
WORKDIR /elgg-src/
RUN wget https://elgg.org/getelgg.php?forward=elgg-${ELGG_VERSION}.zip -O elgg-${ELGG_VERSION}.zip
RUN unzip elgg-${ELGG_VERSION}.zip -d .
WORKDIR /elgg-src/elgg-${ELGG_VERSION}/
COPY . ${ELGG_PATH}

WORKDIR /

# Set perms for the Elgg data root
RUN mkdir ${ELGG_DATA_ROOT}
RUN chown -R www-data:www-data ${ELGG_DATA_ROOT}
RUN chmod 770 -R ${ELGG_DATA_ROOT}

# Set perms for the Elgg path
RUN chown -R www-data:www-data ${ELGG_PATH}
RUN chmod 770 -R ${ELGG_PATH}
#RUN chown -R www-data:www-data "${ELGG_PATH}elgg-config/"

# expose ports
EXPOSE 80 443 3306 6379
