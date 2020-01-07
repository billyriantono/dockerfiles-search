FROM amgrade/php
MAINTAINER Artem Berdyshev "a.berdyshev@amgrade.com"


ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get -yq install \
        curl \
        apache2 \
        libapache2-mod-php5 \
        libapache2-mod-rpaf && \
    rm -rf /var/lib/apt/lists/*

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
COPY default /etc/apache2/sites-available/000-default.conf
COPY php.ini /etc/php5/apache2/php.ini

ADD envvars /etc/apache2/envvars

RUN a2enmod rewrite rpaf

# Add image configuration and scripts
ADD run.sh /run.sh
RUN chmod 755 /*.sh


EXPOSE 80 443 9000
WORKDIR /var/www/html
CMD ["/run.sh"]

