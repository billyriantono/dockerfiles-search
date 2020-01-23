FROM php:7.3.8-apache
RUN docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-enable mysqli pdo pdo_mysql 


COPY msmtprc /usr/local/etc/msmtprc

RUN chown www-data:www-data /usr/local/etc/msmtprc
RUN chmod 600 /usr/local/etc/msmtprc

RUN mkdir -p /usr/share/man/man1

 # Install needed php extensions: ldap
RUN apt-get update \
    && apt-get install -y -q --no-install-recommends \
    libldap2-dev -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libpng-dev \
    libmemcached-dev \
    zlib1g-dev \
    libicu-dev \
    libpq-dev  \
    libssh2-1-dev \
    libmagickwand-dev \
    libxml2-dev \
    libzip-dev \
    zip \
    msmtp  \
    openssl \
    ca-certificates \
    #default-jre \
    pdftk \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*  
    # && sed -ri -e 's/^(host ).*/\1%%SMTP_HUB%%/' -e 's/^#(FromLineOverride)/\1/' /etc/msmtprc
    # configure ssmtp to read from env so php's mail() function will work out of the box. 

	
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap \
    && docker-php-ext-install zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd 

# Enable Apache ldap auth module
RUN a2enmod authnz_ldap

RUN sed -i 's/LEVEL=2/LEVEL=1/g' /etc/ssl/openssl.cnf

RUN cp /usr/local/etc/msmtprc /etc/msmtprc
