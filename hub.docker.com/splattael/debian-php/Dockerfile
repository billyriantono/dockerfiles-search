FROM debian:jessie
MAINTAINER Peter Suschlik <peter@suschlik.de>

ENV RELEASE_DATE 2015-07-03
ENV DEBIAN_FRONTEND noninteractive
ENV APACHE_HTTPD "exec /usr/sbin/apache2"

RUN \
  apt-get -qq update && \
  apt-get -qq install \
    apache2 php5 ssmtp libapache2-mod-php5 php5-mysql php5-json php5-curl php5-gd \
    && \
  apt-get clean

VOLUME /var/www
VOLUME ["/etc/apache2/sites-available", "/etc/apache2/sites-enabled"]

EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
