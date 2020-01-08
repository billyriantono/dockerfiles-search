FROM ubuntu:14.04
MAINTAINER Mohammad Zolfaghari <zidom72@gmail.com>

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update -y
RUN apt-get install -y software-properties-common

RUN add-apt-repository -y ppa:ondrej/php5-5.6

RUN apt-get update
RUN apt-get -y install php5-fpm php5-mysql php5-pgsql php5-sqlite \
	php5-curl php5-gd php5-gmp php5-mcrypt php5-memcached php5-imagick \
	php5-intl php5-imap php5-tidy php5-dev php5-cli php-pear

RUN pecl install mongo
RUN echo "extension=mongo.so" >> /etc/php5/mods-available/mongo.ini
RUN echo "extension=mongo.so" >> /etc/php5/fpm/conf.d/20-mongo.ini
RUN echo "extension=mongo.so" >> /etc/php5/cli/conf.d/20-mongo.ini

RUN sed -i "s/;date.timezone =.*/date.timezone = UTC/" /etc/php5/fpm/php.ini
RUN sed -i "s/;date.timezone =.*/date.timezone = UTC/" /etc/php5/cli/php.ini
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php5/fpm/php.ini
RUN sed -i "s/;daemonize = yes/daemonize = no/" /etc/php5/fpm/php-fpm.conf
RUN sed -i "s%listen = /var/run/php5-fpm.sock%listen = 0.0.0.0:9000%" /etc/php5/fpm/pool.d/www.conf

ADD start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

RUN mkdir /var/www

WORKDIR /var/www

VOLUME ["/var/www"]
EXPOSE 9000

CMD ["start-container"]
