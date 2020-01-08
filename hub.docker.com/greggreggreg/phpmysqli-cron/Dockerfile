FROM php:7.2-apache
RUN docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-enable mysqli pdo pdo_mysql 

RUN apt-get update && apt-get install -y libc-client-dev libkrb5-dev && rm -r /var/lib/apt/lists/*
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap

RUN apt-get update && apt-get install -y exim4-daemon-light

COPY exim.conf /etc/exim4/update-exim4.conf.conf

 # Install needed php extensions: ldap
RUN apt-get update && apt-get install libldap2-dev -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libpng-dev \
    libmemcached-dev \
    zlib1g-dev \
    libicu-dev \
    libpq-dev \
    libssh2-1-dev \
    libxml2-dev \
    libmagickwand-dev  \
    cron \
    #ssmtp \
    vim  \
    zip \
    && rm -rf /var/lib/apt/lists/*  
    # configure ssmtp to read from env so php's mail() function will work out of the box. 
    #&& sed -ri -e 's/^(mailhub=).*/\1%%SMTP_HUB%%/' -e 's/^#(FromLineOverride)/\1/' /etc/ssmtp/ssmtp.conf
    # && echo 'sendmail_path = /usr/sbin/sendmail -t -i' >> /usr/local/etc/php/conf.d/sendmail.ini
    # ssmtp  \
  
RUN pecl install mcrypt-1.0.1 && docker-php-ext-enable mcrypt	 
	 
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap \
    && docker-php-ext-install zip
   
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
 
# Add crontab file in the cron directory
ADD crontab /etc/cron.d/hello-cron

# Give execution rights on the cron job
RUN chmod 0644 /etc/cron.d/hello-cron

# Apply cron job
RUN crontab /etc/cron.d/hello-cron



COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
RUN chmod +x /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT [ "docker-entrypoint.sh" ]




# Run the command on container startup
CMD ["cron", "-f"]
