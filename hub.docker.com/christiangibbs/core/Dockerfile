FROM ubuntu:16.04

MAINTAINER Christian Gibbs <christian@gibbsi.co.uk>

ADD . /app
WORKDIR /app

RUN apt-get update -yq && \
    apt-get upgrade -yq

# Install apache2
RUN apt-get install -yq apache2

# Enable required apache2 mods
RUN a2enmod rewrite

# Install MariaDB
Run apt-get install -yq mariadb-server

# Install PHP7.0 and Modules
RUN apt-get install -yq php7.0 \
                        libapache2-mod-php7.0 \
                        php7.0-intl \
                        php7.0-gd \
                        php7.0-mysql \
                        php7.0-xml \
                        php7.0-mbstring \
                        php7.0-bcmath \
                        php7.0-mcrypt \
                        php7.0-cli \
                        php7.0-curl

RUN apt-get clean

CMD ["/bin/bash"]
