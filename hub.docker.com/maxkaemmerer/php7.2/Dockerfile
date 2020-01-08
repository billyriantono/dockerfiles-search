FROM ubuntu:xenial

ENV LC_ALL=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y software-properties-common \
    && add-apt-repository ppa:ondrej/php \
    && apt-get update 
RUN apt-get install -y apache2 git wget curl
RUN apt-get install -y php7.2 php7.2-common php7.2-cli php7.2-fpm php7.2-dom php7.2-pgsql php7.2-mbstring php7.2-zip php7.2-mysql

EXPOSE 80 443

WORKDIR /var/www/html
COPY index.php index.php
RUN rm index.html
ADD 000-default.conf /etc/apache2/sites-enabled/000-default.conf

RUN apt-get install -y libapache2-mod-php7.2 libapache2-mod-fastcgi \
    && a2enconf php7.2-fpm \
    && a2enmod php7.2 \
    && a2enmod rewrite \
    && a2enmod actions fastcgi alias proxy_fcgi \
    && service php7.2-fpm start \
    && service apache2 restart

CMD service php7.2-fpm start && /usr/sbin/apache2ctl -D FOREGROUND
