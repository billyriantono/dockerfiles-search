FROM ubuntu:14.04
MAINTAINER Miloš Kozák <milos.kozak@lejmr.com>

RUN apt-get update \
    && apt-get -y install apache2 \
                          libapache2-mod-fcgid \
                          libxslt1.1 \
                          libpq5 \
                          libmcrypt4 \
                          libjpeg-turbo8 \
                          libcurl3 \
                          libfreetype6 \
                          apache2-suexec-custom \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


COPY php-5.4.tar.bz2 /tmp
RUN /usr/sbin/a2dismod 'mpm_*' \
    && /usr/sbin/a2enmod mpm_prefork \
    && /usr/sbin/a2enmod rewrite \
    && /usr/sbin/a2enmod fcgid \
    && /usr/sbin/a2enmod suexec \
    && mkdir -p /var/www/fcgi/php5 \
    && useradd -b /var/www/html/ web

RUN tar xjf /tmp/php-5.4.tar.bz2 -C /opt \
    && /bin/rm /tmp/php-5.4.tar.bz2

WORKDIR /var/www
COPY fcgi/php5-fcgi-starter  fcgi/php5-fcgi-starter
COPY fcgi/php5/browscap.ini fcgi/php5/browscap.ini
COPY fcgi/php5/php.ini fcgi/php5/php.ini
COPY default-site.conf /etc/apache2/sites-enabled/000-default.conf
COPY apache-php.conf /etc/apache2/conf-enabled/fcgid_easyscp.conf
RUN chown web:web /var/www/fcgi -R

COPY httpd-foreground /usr/bin/
RUN chmod +x /usr/bin/httpd-foreground

EXPOSE 80
CMD ["/usr/bin/httpd-foreground"]