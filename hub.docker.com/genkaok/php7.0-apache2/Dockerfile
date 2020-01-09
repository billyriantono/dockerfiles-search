FROM debian:jessie
MAINTAINER GenkaOk <genkaok@yandex.ru>

VOLUME ["/var/www"]

# Add main repository from production
RUN echo 'deb http://mirror.yandex.ru/debian jessie main contrib non-free\n' > /etc/apt/sources.list
RUN echo 'deb-src http://mirror.yandex.ru/debian jessie main contrib non-free\n' >> /etc/apt/sources.list
RUN echo 'deb http://security.debian.org/ jessie/updates main contrib non-free\n' >> /etc/apt/sources.list
RUN echo 'deb-src http://security.debian.org/ jessie/updates main contrib non-free\n' >> /etc/apt/sources.list
# Add main repository from production

# Install main software
RUN apt-get update && apt-get install -y wget unzip apt-transport-https
# Install main software

# Add extra repository from production
RUN echo 'deb http://packages.dotdeb.org jessie all\n' >> /etc/apt/sources.list
RUN echo 'deb-src http://packages.dotdeb.org jessie all\n' >> /etc/apt/sources.list
RUN wget https://www.dotdeb.org/dotdeb.gpg
RUN apt-key add dotdeb.gpg
# Add extra repository from production

# Install apache2 server
RUN apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install -y \
        apache2 \
        curl \
        php7.0 \
        php7.0-cli \
        php7.0-apcu \
        libapache2-mod-php7.0 \
        php7.0-gd \
        php7.0-json \
        php7.0-ldap \
        php7.0-mbstring \
        php7.0-mysql \
        php7.0-pgsql \
        php7.0-sqlite3 \
        php7.0-xml \
        php7.0-xsl \
        php7.0-zip \
        php7.0-soap \
        php7.0-opcache \
        php7.0-pdo \
        php7.0-curl \
        php7.0-igbinary \
        php7.0-bz2 \
        php7.0-geoip \
        php7.0-imagick \
        php7.0-imap \
        php7.0-mcrypt \
        php7.0-redis \
        php7.0-xmlrpc

# Install composer
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer

# Copy config files
COPY apache_default /etc/apache2/sites-available/000-default.conf
COPY run /usr/local/bin/run
COPY php.ini /etc/php/7.0/apache2/php.ini
COPY php.ini /etc/php/7.0/cli/php.ini

RUN chmod +x /usr/local/bin/run
RUN a2enmod rewrite

EXPOSE 80
CMD ["/usr/local/bin/run"]