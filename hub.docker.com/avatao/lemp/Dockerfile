FROM avatao/ubuntu:14.04

ENV NGINX_VERSION 1.8.1-1~trusty

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
	&& echo "deb http://nginx.org/packages/ubuntu/ trusty nginx" >> /etc/apt/sources.list \
	&& apt-get update \
	&& apt-get install -qy \
		ca-certificates \
		nginx=${NGINX_VERSION} \ 
		gettext-base \
		php5-fpm \
		mariadb-server \
		php-apc \
		php5-mcrypt \
		php5-mysql \
		pwgen \
		supervisor \
	&&	php5enmod mcrypt \
	&& rm -rf /var/lib/apt/lists/* /var/lib/mysql/* \
	&& ln -sf /dev/stderr /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log \
	&& ln -sf /dev/stderr /var/log/php5-fpm.log

COPY ./ /

#setup mysql
RUN mkdir -p /var/run/mysqld /var/log/mysql
RUN chown -R www-data:www-data /var/run/mysqld /var/log/mysql
RUN mysql_install_db --defaults-file=/etc/mysql/conf.d/my.cnf

RUN chmod 664 /var/www/*.* \
	&& chown -R www-data:www-data /var/www \
	&& chown www-data /var/cache/nginx

VOLUME ["/var/lib/mysql", "/var/run/mysqld", "/var/log/mysql"]

VOLUME ["/var/log", "/var/run/php-fpm", "/var/lib/php5", "/var/cache/nginx", "/etc/nginx", "/run"]

EXPOSE 8888
USER www-data
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]


