FROM ubuntu:14.04

RUN apt update && apt install -y php5 php5-redis php5-json php5-fpm php5-mysql php5-mongo php-pear php5-curl && \
        pear install System_Daemon-1.0.0 && \
        apt install -y nginx supervisor vim && \
        rm /etc/init.d/nginx && rm /etc/init.d/php5-fpm && \
        apt-get clean autoclean && \
        apt-get autoremove --yes && \
        rm -rf /var/lib/{apt,dpkg,cache,log}/
