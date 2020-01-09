#Copy from service-newsletter dockerfile
FROM php:7.1-apache
MAINTAINER Gary Gitton <gary.gitton@gmail.com>

ENV ERRORS 0
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update && \
    apt-get -y upgrade

RUN mkdir -p /usr/share/man/man1 && \
    mkdir -p /usr/share/man/man7

RUN apt-get -y install \
    software-properties-common \
    git \
    zip \
    unzip \
    curl \
    wget \
    libjpeg-dev \
    libfreetype6-dev \
    libmcrypt-dev \
    lynx-common \
    lynx \
    libxml2-dev \
    libcurl4-openssl-dev  \
    zlib1g-dev \
    libicu-dev \
    g++ \
    vim \
    supervisor \
    cron \
    postgresql-9.6 \
    libpq-dev \
    libgmp3-dev \
    default-jdk && \
    curl -sS https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.0.0.1744-linux.zip > /opt/sonar-scanner-cli-4.0.0.1744-linux.zip && \
    unzip /opt/sonar-scanner-cli-4.0.0.1744-linux.zip -d /opt && \
    rm -Rf /opt/sonar-scanner-cli-4.0.0.1744-linux.zip && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=usr/include/ && \
    docker-php-ext-install \
        soap \
        bcmath \
        curl  \
        gd \
        iconv \
        intl \
        json \
        mbstring \
        mysqli \
        pdo \
        pdo_mysql \
        session \
        simplexml \
        xml \
        zip \
        mcrypt \
        xmlrpc \
        pgsql \
        pdo_pgsql \
        gmp && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get -y autoclean && \
    apt-get -y clean && \
    apt-get -y autoremove

# Configuration Apache
RUN a2enmod headers expires rewrite && \
    sed -i "s/html/public/g" /etc/apache2/sites-available/000-default.conf && \
    echo "ServerName localhost" >> /etc/apache2/apache2.conf

WORKDIR /var/www

RUN chmod -R +x /usr/local/bin/

## Setup workdir
RUN rm -rf html && \
    mkdir -p -m +w /var/www/logs && \
    mkdir -p /var/www/bootstrap/cache/ && \
    mkdir -p /var/www/storage/framework/cache/data/ && \
    mkdir -p /var/www/storage/framework/sessions/ && \
    mkdir -p /var/www/storage/framework/testing/ && \
    mkdir -p /var/www/storage/framework/views/ && \
    mkdir -p /var/www/storage/logs/
COPY ./ /var/www/

RUN usermod -u 1000 www-data && \
    chown -R www-data:www-data /var/www

ENV PATH="/opt/sonar-scanner-4.0.0.1744-linux/bin:${PATH}"

CMD entrypoint
