FROM debian:6.0.9

# update APT
ADD sources.list /etc/apt/sources.list

# PHP
RUN chmod 555 /etc/apt/sources.list & apt-get update && apt-get -y install curl php5 php5-cgi php5-dev php5-pgsql php5-mysql php-apc php5-curl php5-gd php5-mcrypt php5-memcached libssl-dev sendmail-bin libtool libc6 php-pear && apt-get -y autoremove && apt-get clean

EXPOSE 9000

ENV PHP_FCGI_CHILDREN       20
ENV PHP_FCGI_MAX_REQUESTS   10000

USER nobody

CMD ["/usr/bin/php5-cgi", "-b", "0.0.0.0:9000"]
