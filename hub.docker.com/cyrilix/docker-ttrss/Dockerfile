FROM debian:jessie
MAINTAINER Cyrille Nofficial<cynoffic@cyrilix.fr>

LABEL version="0.1"
LABEL description="Tiny Tiny RSS web-based news feed (RSS/Atom) reader/aggregator"

RUN     apt-get update &&\
        apt-get upgrade &&\
        apt-get -y install php5-fpm git - php5-pgsql php5-curl php5-gd php5-json &&\
        adduser --system --home /opt/ttrss ttrss

COPY php-fpm/php-fpm.conf /etc/php5/fpm/php-fpm.conf

RUN  git clone https://tt-rss.org/git/tt-rss.git /opt/ttrss

EXPOSE 8080

CMD /usr/sbin/php5-fpm --no-php-ini --fpm-config /etc/php5/fpm/php-fpm.conf --nodaemonize
