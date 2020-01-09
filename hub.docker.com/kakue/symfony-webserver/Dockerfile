FROM php:7-apache
LABEL maintainer=KarstenKuehn<karstenkuehn@hotmail.de>
# install some extensions
RUN export DEBIAN_FRONTEND=noninteractive && apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libxml2 \
        libxml2-dev \
        libicu-dev \
        wget \
        mysql-client \
        unzip \
        git \
        postfix \
        cron \
        vim \
        pdftk \
        inetutils-syslogd \
        libxrender1 \
        libfontconfig1 \
        libapache2-mod-rpaf \
        logrotate \
    && docker-php-ext-install -j$(nproc) mysqli iconv intl mcrypt opcache pdo pdo_mysql mbstring soap xml zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
# adding some configurations for apache, php
ADD wkhtmltox/bin/wkhtmltopdf /usr/local/bin/wkhtmltopdf
ADD wkhtmltox/bin/wkhtmltoimage /usr/local/bin/wkhtmltoimage
ADD wkhtmltox/lib/libwkhtmltox.so /usr/local/lib/libwkhtmltox.so
ADD wkhtmltox/lib/libwkhtmltox.so.0 /usr/local/lib/libwkhtmltox.so.0
ADD wkhtmltox/lib/libwkhtmltox.so.0.12 /usr/local/lib/libwkhtmltox.so.0.12
ADD wkhtmltox/lib/libwkhtmltox.so.0.12.4 /usr/local/lib/libwkhtmltox.so.0.12.4
ADD php/php.ini /usr/local/etc/php/php.ini
ADD apache/apache2.conf /etc/apache2/apache2.conf
ADD apache/logrotate-apache2 /etc/logrotate.d/apache2
ADD apache/symfony-apache.conf /etc/apache2/sites-available/000-default.conf
ADD mail/main.cf /etc/postfix/main.cf


RUN echo Europe/Berlin > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata
RUN echo 'de_DE ISO-8859-1\n\
de_DE.UTF-8 UTF-8\n\
de_DE@euro ISO-8859-15\n\
en_GB ISO-8859-1\n\
en_GB.ISO-8859-15 ISO-8859-15\n\
en_US ISO-8859-1\n\
en_US.ISO-8859-15 ISO-8859-15\n\
en_US.UTF-8 UTF-8\n\
fr_FR ISO-8859-1\n\
fr_FR.UTF-8 UTF-8\n\
fr_FR@euro ISO-8859-15\n\
nl_BE ISO-8859-1\n\
nl_BE.UTF-8 UTF-8\n\
nl_BE@euro ISO-8859-15\n\
nl_NL ISO-8859-1\n\
nl_NL.UTF-8 UTF-8\n\
nl_NL@euro ISO-8859-15\n'

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR  /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

RUN usermod -u 1000 www-data

# Enable rewrite and install composer for use in symfony
RUN a2enmod rewrite && a2enmod rpaf && a2enmod ssl && mkdir /composer-setup && wget https://getcomposer.org/installer -P /composer-setup && php /composer-setup/installer --install-dir=/usr/bin && rm -Rf /composer-setup && curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony && chmod a+x /usr/local/bin/symfony

RUN echo -e "$(hostname -i)\t$(hostname) $(hostname).localhost" >> /etc/hosts

ADD startup.sh /usr/local/startup.sh  
RUN chmod +x /usr/local/startup.sh

WORKDIR /var/www/html
VOLUME ["/var/www/html"]
VOLUME ["/var/log/apache2"]

EXPOSE 80
EXPOSE 443

CMD ["/usr/local/startup.sh"]


