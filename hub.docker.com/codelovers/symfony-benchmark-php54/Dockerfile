FROM debian:wheezy

MAINTAINER Daniel Holzmann <daniel@codelovers.at>


ENV TIMEZONE Europe/Vienna
ENV PORT 9000
ENV MEMORY_LIMIT 256M
ENV MAX_EXECUTION_TIME 180

# install php
RUN apt-get update -qq && apt-get upgrade -y -qq
RUN apt-get install -y sudo php5 php5-fpm php-pear php5-dev php-apc php5-common php5-json php5-memcache php5-memcached php5-xsl php5-mcrypt php5-mysql php5-cli php5-gd php5-intl php5-curl git ruby build-essential

# install mongo extension
RUN sudo pecl install mongo

ADD conf/php.ini /etc/php5/fpm/php.ini

# Set timezone
RUN echo $TIMEZONE > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata
RUN sed -i "s@^;date.timezone =.*@date.timezone = $TIMEZONE@" /etc/php5/*/php.ini

# Set memory limit
RUN sed -i "s@^memory_limit =.*@memory_limit = $MEMORY_LIMIT@" /etc/php5/fpm/php.ini

# Set Max execution time
RUN sed -i "s@^max_execution_time = .*@max_execution_time = $MAX_EXECUTION_TIME@" /etc/php5/fpm/php.ini

# Disable daemonizeing php-fpm
RUN sed -i "s@^;daemonize = yes*@daemonize = no@" /etc/php5/fpm/php-fpm.conf

# Set listen socket for php-fpm
ADD conf/www.conf /etc/php5/fpm/pool.d/www.conf
RUN sed -i "s@listen = 127.0.0.1:9000@listen = ${PORT};@" /etc/php5/fpm/pool.d/www.conf

ADD run.sh /run.sh
RUN chmod +x /run.sh

RUN mkdir -p /var/log/php-fpm

ENTRYPOINT ["/run.sh"]

EXPOSE 9000
