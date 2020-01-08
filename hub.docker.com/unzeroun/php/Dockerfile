FROM unzeroun/base

ENV DEBIAN_FRONTEND noninteractive

RUN aptitude update
RUN aptitude -y install php5-cli php5-mcrypt php5-curl php5-xdebug php5-dev php5-mysql php5-intl php5-gd php5-mongo \
                        php5-memcache php5-memcached

ADD php.ini /etc/php5/cli/php.ini
