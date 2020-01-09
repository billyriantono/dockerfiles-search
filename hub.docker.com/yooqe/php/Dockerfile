FROM yooqe/base

ENV DEBIAN_FRONTEND noninteractive
RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list
RUN aptitude update
RUN aptitude -y install php5-cli php5-mcrypt php5-curl php5-xdebug php5-dev php5-mysql php5-intl php5-gd php5-mongo \
                        php5-memcache php5-memcached php7.0-mbstring

ADD php.ini /etc/php5/cli/php.ini
