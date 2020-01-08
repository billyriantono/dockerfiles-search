FROM debian:jessie

MAINTAINER Codete <ci@codete.com>

RUN apt-get update && \
    apt-get install -y ccze php5 php5-fpm php5-cli php5-dev php5-common php5-curl php5-mysql && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    sed -i "s/;date\.timezone =.*/date\.timezone = Europe\/Warsaw/" /etc/php5/cli/php.ini && \
    sed -i "s/variables_order =.*/variables_order = \"EGPCS\"/" /etc/php5/cli/php.ini && \
    sed -i "s/;date\.timezone =.*/date\.timezone = Europe\/Warsaw/" /etc/php5/fpm/php.ini && \
    sed -i "s/variables_order =.*/variables_order = \"EGPCS\"/" /etc/php5/fpm/php.ini && \
    sed -i "s/listen =.*/listen = 0\.0\.0\.0:9000/" /etc/php5/fpm/pool.d/www.conf

VOLUME ["/etc/php5/cli", "/etc/php5/fpm"]

EXPOSE 9000

CMD php -a
