FROM phusion/baseimage:0.9.15

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get -yq install \
        curl \
        apache2 \
        libapache2-mod-php5 \
        php5-mysql \
        php5-gd \
        php5-curl \
        php-pear \
        php-apc && \
    rm -rf /var/lib/apt/lists/*
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add image configuration and scripts
ADD run.sh /run.sh
RUN chmod 755 /*.sh

COPY apache2.conf /etc/apache2/apache2.conf
RUN rm -rf /etc/apache2/sites-enabled/*

RUN adduser --disabled-password --gecos '' deploy

ADD php.ini /etc/php5/apache2/php.ini

RUN a2enmod rewrite 

EXPOSE 80
WORKDIR /app
CMD ["/run.sh"]