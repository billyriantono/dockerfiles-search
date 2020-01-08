FROM ubuntu:15.10

MAINTAINER Alex Oleshkevich <alex.oleshkevich@gmail.com>

RUN useradd -M -u 1000 docker
RUN apt-get update && apt-get install -y php5-fpm php5-cli php5-enchant php5-facedetect \
    php5-exactimage php5-gd php5-gdcm php5-gearman php5-geoip php5-gmp php5-imagick php5-imap \
    php5-intl php5-json php5-mcrypt php5-mongo php5-mysqlnd php5-oauth php5-odbc \
    php5-pecl-http php5-readline php5-phpdbg php5-solr php5-sqlite php5-ssh2 php5-symfony-debug \
    php5-xdebug php5-xhprof php5-xmlrpc php5-curl php5-ldap php5-memcache php5-memcached
RUN apt-get clean && apt-get autoremove
WORKDIR /root
ADD ./bootstrap.sh ./bootstrap.sh
RUN chmod +x ./bootstrap.sh
EXPOSE 9000
CMD ["./bootstrap.sh"]
