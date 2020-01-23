################################
#                              #
#   Ubuntu - PHP 7.0 CLI+FPM   #
#                              #
################################

FROM ubuntu:xenial

MAINTAINER IT DEV GROUP <info@it-devgroup.com>

LABEL Vendor="itdevgroup"
LABEL Description="PHP-FPM v7.0.30"
LABEL Version="1.0.0"

ENV ITDEVGROUP_TIME_ZONE Europe/Kiev

RUN apt-get update -yqq \
    && apt-get install -yqq \
	ca-certificates \
    git \
    gcc \
    make \
    wget \
    mc \
    curl \
    cron \
    zip \
    supervisor 

RUN DEBIAN_FRONTEND=noninteractive apt-get -y dist-upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install python-software-properties
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install software-properties-common
RUN DEBIAN_FRONTEND=noninteractive LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

## Install php7.0 extension
RUN apt-get update -yqq \
    && apt-get install -yqq \
        php7.0-pgsql \
	php7.0-mysql \
	php7.0-opcache \
	php7.0-common \
	php7.0-mbstring \
	php7.0-mcrypt \
	php7.0-soap \
	php7.0-cli \
	php7.0-intl \
	php7.0-json \
	php7.0-xsl \
	php7.0-imap \
	php7.0-ldap \
	php7.0-curl \
	php7.0-gd  \
        php7.0-zip  \
	php7.0-dev \
        php7.0-fpm \
	php7.0-redis \
	php7.0-memcached \
	php7.0-mongodb \
        php7.0-imagick \
        php7.0-bcmath \ 
        php7.0-zmq \
        php7.0-apcu \
    && apt-get install pkg-config \
    && apt-get install -y -q --no-install-recommends \
       ssmtp

# ioncube loader
RUN curl -fSL 'http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz' -o ioncube.tar.gz \
    && mkdir -p ioncube \
    && tar -xf ioncube.tar.gz -C ioncube --strip-components=1 \
    && rm ioncube.tar.gz \
    && mv ioncube/ioncube_loader_lin_7.0.so /usr/lib/php/20151012/ioncube_loader_lin_7.0.so \
    && rm -r ioncube

# Add default timezone
RUN echo $ITDEVGROUP_TIME_ZONE > /etc/timezone \
    && echo "date.timezone=$ITDEVGROUP_TIME_ZONE" > /etc/php/7.0/cli/conf.d/timezone.ini

# Download browscap.ini
RUN mkdir /var/lib/browscap \
    && wget http://browscap.org/stream?q=BrowsCapINI -O /var/lib/browscap/browscap.ini

## Install composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

# Copy our config files for php7.0 fpm and php7.0 cli
COPY php-conf/php.ini /etc/php/7.0/cli/php.ini
COPY php-conf/php-fpm.ini /etc/php/7.0/fpm/php.ini
COPY php-conf/php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf
COPY php-conf/www.conf /etc/php/7.0/fpm/pool.d/www.conf

# Download and install wkhtmltopdf
RUN apt-get install xvfb libfontconfig wkhtmltopdf -y

## Create xvfb wrapper for wkhtmltopdf and create special sh script
RUN touch /usr/local/bin/wkhtmltopdf \
    && chmod a+x /usr/local/bin/wkhtmltopdf \
    && echo 'xvfb-run -a -s "-screen 0 640x480x16" wkhtmltopdf "$@"' > /usr/local/bin/wkhtmltopdf \
    && chmod a+x /usr/local/bin/wkhtmltopdf


RUN usermod -aG www-data www-data
# Reconfigure system time
RUN  dpkg-reconfigure -f noninteractive tzdata

# Clear all packages and temp files
RUN	apt-get clean -yqq \
	&& apt-get purge php7.0-dev -yqq \
	&& apt-get purge git -yqq \
	&& apt-get purge gcc -yqq \
	&& apt-get purge make -yqq \
	&& apt-get purge wget -yqq \
	&& apt-get purge curl -yqq

RUN rm -rf /var/lib/apt/lists/* \
	&& rm -rf /tmp/* \
	&& apt-get clean -yqq

COPY start.sh /start.sh
RUN chmod +x /start.sh

CMD ["/start.sh"]

WORKDIR /var/www/itdevgroup

EXPOSE 9000