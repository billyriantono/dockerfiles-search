FROM debian:8.8

RUN \
	apt-get update \
        && apt-get install -y wget \
	&& echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list \
	&& wget https://www.dotdeb.org/dotdeb.gpg \
	&& apt-key add dotdeb.gpg \
	&& apt-get update \
	&& apt-get install -y php7.0 php7.0-fpm php7.0-zip php7.0-xml php7.0-gd php7.0-curl php7.0-mbstring php7.0-mysql

COPY conf/php.ini /etc/php/7.0/lib/php.ini
COPY conf/www.conf /etc/php/7.0/fpm/pool.d/www.conf
COPY conf/php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf

EXPOSE 9000

CMD /usr/sbin/php-fpm7.0 --nodaemonize
