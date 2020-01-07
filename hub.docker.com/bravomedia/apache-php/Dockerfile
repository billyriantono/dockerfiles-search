FROM ubuntu:14.04

RUN rm -vf /var/lib/apt/lists/*
RUN apt-get update
RUN apt-get install -y \
    php5 \
    php-apc \
    php5-cli \
    php5-common \
    php5-curl \
    php5-fpm \
    php5-gd \
    php5-gmp \
    php5-imagick \
    php5-intl \
    php5-json \
    php5-mcrypt \
    php5-mysql \
    php5-sqlite \
    php5-tidy \
    php5-xdebug \
    php5-xmlrpc \
    apache2 \
    libapache2-mod-php5 \
    curl \
    unzip \
    git

RUN ln -sf /dev/stderr /var/log/apache2/error.log
RUN ln -sf /dev/stdout /var/log/apache2/access.log
RUN ln -sf /dev/stdout /var/log/apache2/other_vhosts_access.log
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod expires
RUN a2enmod headers
RUN a2enmod php5
RUN rm /etc/apache2/sites-enabled/*
RUN mv /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/050-default.conf
RUN a2ensite 050-default
RUN apache2ctl configtest
RUN touch /etc/apache2/mime.types

ADD composer-setup.sh /
RUN chmod +x composer-setup.sh
RUN /composer-setup.sh

EXPOSE 80
EXPOSE 443

ADD start.sh /
RUN chmod +x start.sh

CMD ["/start.sh"]
