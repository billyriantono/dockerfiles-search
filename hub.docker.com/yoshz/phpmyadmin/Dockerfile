FROM yoshz/apache-php:5.5
MAINTAINER Yosh de Vos "yosh@elzorro.nl"
ENV RELEASE_DATE 2015-12-06

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get -yq install phpmyadmin && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/*

ADD default-vhost.conf /etc/apache2/sites-available/000-default.conf
ADD config-db.php /etc/phpmyadmin/config-db.php
