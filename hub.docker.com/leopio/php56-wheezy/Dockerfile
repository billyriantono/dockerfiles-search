FROM debian:wheezy

RUN apt-get update -qq && apt-get upgrade -y
RUN apt-get install nano wget ca-certificates -qq

RUN wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb
RUN dpkg -i dumb-init_*.deb

RUN apt-get update \
  && apt-get install -y --force-yes \
  php5 \
  php5-fpm \
  php5-cli \
  php5-pgsql \
  php5-mcrypt \
  php5-curl \
  php5-gd \
  php5-intl

EXPOSE 9000

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["php5-fpm", "-c", "/etc/php5/fpm", "--fpm-config", "/etc/php5/fpm/php-fpm.conf", "-F"]
RUN php -v
