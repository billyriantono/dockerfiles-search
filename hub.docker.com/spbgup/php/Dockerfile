FROM php:5.6

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install git
RUN apt-get update \
    && apt-get -y install git \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Add php-ldap
RUN apt-get update && apt-get install -y unzip libldap2-dev\
	&& apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* \
	&& docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap

# Add php5-sybase
RUN apt-get update && apt-get install -y freetds-dev \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
RUN docker-php-ext-configure sybase_ct --with-sybase-ct=/usr \
	&& docker-php-ext-install sybase_ct
	
# Add php5-xdebug
RUN pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug
	
# Add php5-pcntl
RUN docker-php-ext-install pcntl	

# Add php5-pdo-mysql
RUN docker-php-ext-install pdo pdo_mysql