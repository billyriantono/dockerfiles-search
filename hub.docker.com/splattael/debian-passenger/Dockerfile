FROM debian:wheezy
MAINTAINER Peter Suschlik <peter@suschlik.de>

ENV RELEASE_DATE 2015-07-03
ENV DEBIAN_FRONTEND noninteractive
ENV APACHE_HTTPD "exec /usr/sbin/apache2"

RUN apt-get -qq update
RUN \
  apt-get -qq install \
    apache2 ruby1.8 ruby-passenger libapache2-mod-passenger \
    libmysqlclient-dev \
    libmagickcore5 libmagickcore-dev libmagickwand-dev libmagickwand5 \
  && apt-get clean

RUN echo "gem: --no-rdoc --no-ri" > /root/.gemrc

VOLUME [ "/var/www", "/etc/apache2/sites-enabled", "/var/lib/gems", "/usr/local" ]

EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
