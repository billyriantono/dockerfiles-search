FROM debian:stretch-slim

# Update system and install necessary components like nginx and php
RUN apt-get update \ 
	&& apt-get upgrade -y \
	&& apt-get install -y --no-install-recommends nginx php-fpm php-mysql supervisor \
	&& rm -rf /var/lib/apt/lists/*

VOLUME ["/var/www/html"]

COPY nginx.default.conf /etc/nginx/sites-available/default
COPY php-fpm.conf /etc/php/7.0/fpm/pool.d/www.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY docker-entrypoint.sh /

ADD https://wordpress.org/latest.tar.gz /root

RUN chmod u+x /docker-entrypoint.sh && service php7.0-fpm start

EXPOSE 80

ENTRYPOINT ["/docker-entrypoint.sh"]	
