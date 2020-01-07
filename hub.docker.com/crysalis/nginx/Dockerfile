FROM playkot/debian:jessie

ENV DEBIAN_FRONTEND noninteractive 

RUN apt-get update \ 
	&& apt-get install -y wget --no-install-recommends \
	&& echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list.d/dotdeb.org.list \
	&& echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list.d/dotdeb.org.list \
	&& wget -O- http://www.dotdeb.org/dotdeb.gpg | apt-key add - \
	&& apt-get update -y \
	&& apt-get install -y --no-install-recommends\
		nginx \
		php5-fpm \
		php-pear \
		php-apc \
		php5-curl \
		php5-dev \
		php5-gd \
		php5-mysql \
		php5-memcached \
		php5-redis \
		php5-mongo \
		supervisor \
	&& rm -rf /var/lib/apt/lists/* \
	&& apt-get purge $(aptitude search '~i!~M!~prequired!~pimportant!~R~prequired!~R~R~prequired!~R~pimportant!~R~R~pimportant!busybox!grub!initramfs-tools' | awk '{print $2}') \
	&& apt-get purge -y wget \ 
	&& apt-get autoremove -y \
	&& apt-get clean -y 

ADD /etc /etc
ADD ./index.php /var/www/index.php
RUN echo "daemon off;" >> /etc/nginx/nginx.conf \
	&& chown -Rf www-data.www-data /var/www/

RUN sed -i 's/;daemonize = yes/daemonize = no/g' /etc/php5/fpm/php-fpm.conf

ADD ./start.sh /start.sh
RUN chmod 755 /start.sh

EXPOSE 80
ENTRYPOINT /start.sh
