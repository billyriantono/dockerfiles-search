FROM php:7.0-apache

# Based on the official Wordpress docker file

RUN a2enmod rewrite expires

# install the PHP extensions we need
RUN apt-get update && apt-get install -y git libpng-dev libjpeg-dev zlib1g-dev && rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& docker-php-ext-install gd mysqli opcache zip mbstring exif

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=60'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

ENV GRAV_VERSION 1.5.1
RUN curl -o grav.tar.gz -SL https://github.com/getgrav/grav/archive/${GRAV_VERSION}.tar.gz \
	&& mkdir -p /tmp/grav \
	&& tar -xzf grav.tar.gz -C /tmp \
	&& rsync -a /tmp/grav-${GRAV_VERSION}/ /var/www/html --exclude user \
	&& /var/www/html/bin/grav install \
	&& chown -R www-data:www-data /var/www/html

RUN cd /var/www/html && bin/gpm install -f -y admin lingonberry comments jscomments

ENV DEBIAN_FRONTEND noninteractive
ENV LETSENCRYPT_HOME /etc/letsencrypt
ENV DOMAINS "arnu.de"
ENV WEBMASTER_MAIL "simon@arnu.de"

RUN mkdir -p  /etc/container_environment
# Manually set the apache environment variables in order to get apache to work immediately.
RUN echo $WEBMASTER_MAIL > /etc/container_environment/WEBMASTER_MAIL && \
    echo $DOMAINS > /etc/container_environment/DOMAINS && \
    echo $LETSENCRYPT_HOME > /etc/container_environment/LETSENCRYPT_HOME

CMD ["/sbin/my_init"]
RUN echo 'deb http://ftp.debian.org/debian stretch-backports main' >> /etc/apt/sources.list && \
    apt-get -y update && \
    apt-get install -q -y python-certbot-apache -t stretch-backports && \
    apt-get clean
RUN a2enmod ssl

#RUN git clone https://github.com/letsencrypt/letsencrypt
#RUN cd letsencrypt && ./letsencrypt-auto --apache -d arnu.de
COPY default-ssl.conf /etc/apache2/sites-available/
RUN mkdir -p /root/certs/
RUN cd /root/certs/ && openssl req -nodes -newkey rsa:4096 -x509 -sha256 -days 365 -nodes -keyout DummyKey.key -out DummyCertificate.crt -subj "/C=DE/ST=nv/L=nv/O=SDummy Network/OU=nv/CN=dummy.org" && chmod 400 /root/certs/DummyKey.key
RUN a2ensite default-ssl.conf
COPY docker-entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2-foreground"]
