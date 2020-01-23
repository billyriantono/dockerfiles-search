# for info check the README file
FROM debian

LABEL maintainer="oferraro@getfinancing.com"
LABEL version="2.2.4"
LABEL description="Basic PHP/Apache Image to start from"

ENV WORKDIR /var/www/html/
WORKDIR $WORKDIR
ENV PHP_VERSION 7.2

RUN apt-get update && apt-get install -y apache2 openssl ca-certificates  \
    php-soap git curl wget

RUN apt-get install -y apt-transport-https lsb-release ca-certificates && \
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list' && \
    apt-get update && apt-get -y install php$PHP_VERSION \
    php$PHP_VERSION-mbstring php$PHP_VERSION-xml php$PHP_VERSION-zip php$PHP_VERSION-mysql \
    php$PHP_VERSION-bcmath php$PHP_VERSION-gd php$PHP_VERSION-common php$PHP_VERSION-curl php$PHP_VERSION-intl

# Define composer home, install composer 
ENV COMPOSER_HOME /var/www/.composer/
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

COPY httpd-foreground /usr/local/bin/ 
RUN chmod u+x /usr/local/bin/httpd-foreground \
	&& rm /etc/apache2/sites-enabled/000-default.conf 

COPY 000-default.conf /etc/apache2/sites-enabled/000-default.conf

# Clean unnecesary files, create composer cache folder, set permissions
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    chsh -s /bin/bash www-data && \
    rm -rf $WORKDIR/* && \
    chown -R www-data:www-data /var/www/ && \
    find /var/www/ -type d -exec chmod 775 {} \; && \
    find /var/www/ -type d -exec chmod g+s {} \; && \
    find /var/www/ -type f -exec chmod 664 {} \; 

EXPOSE 80

CMD ["/usr/local/bin/httpd-foreground"]
