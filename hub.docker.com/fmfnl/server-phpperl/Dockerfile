FROM php:5.6-apache-jessie
LABEL maintainer="Comcie <comcie@fmf.nl>"

RUN apt-get update && apt-get -y install \
    cpanminus \
    curl \
    libapache2-mod-perl2 \
    libdata-printer-perl \
    libdbd-mysql-perl \
    libdbi-perl \
    libfile-slurp-perl \
    libgetopt-long-descriptive-perl \
    libhtml-template-perl \
    libhttp-negotiate-perl \
    liblwp-useragent-determined-perl \
    libtest-strict-perl \
    libwww-mechanize-perl \
    libxml-libxml-perl \
    libxml-simple-perl \
    libxml-twig-perl

RUN docker-php-ext-install mysql mysqli

COPY block-files.conf /etc/apache2/conf-available/

RUN a2enmod rewrite cgi && a2enconf block-files
RUN ln -s /var/www/html /fmf