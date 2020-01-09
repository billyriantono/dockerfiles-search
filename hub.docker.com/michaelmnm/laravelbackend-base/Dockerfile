FROM php:7-fpm
MAINTAINER Michael Mandato <mmandato@helloencom.co>

ENV TERM=xterm-256color

RUN apt-get update && \
	apt-get install -y \
	-o APT::Install-Recommended=false -o APT::Install-Suggestes=false \
	libmcrypt-dev mysql-client gzip zip git && \
	docker-php-ext-install mcrypt pdo_mysql

ADD scripts/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
LABEL application=laravelbackend