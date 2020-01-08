FROM ubuntu:trusty

ENV DEBIAN_FRONTEND noninteractive

# Configure timezone for the logs
RUN echo "Europe/Berlin" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update && apt-get install -y \
	php5-fpm \
	php5-cli \
	php5-curl \
	php5-imagick \
    php5-mysql

ADD config/php-fpm.ini /etc/php5/fpm/php.ini
ADD config/php-cli.ini /etc/php5/cli/php.ini
ADD config/pool-www.conf /etc/php5/fpm/pool.d/www.conf

EXPOSE 9000
ENTRYPOINT ["php5-fpm","-F"]
