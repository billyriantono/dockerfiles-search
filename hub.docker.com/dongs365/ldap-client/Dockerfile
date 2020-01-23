FROM alpine:3.10.3
MAINTAINER anonymous
RUN apk update \
    && apk add \
	--no-cache \
	php7 \
	php7-fpm \
	php7-ldap \
	php7-phalcon \
	nginx \
	supervisor \
    && rm -rf /var/cache/apk/* \
    && mkdir /run/nginx \
    && touch /run/nginx/nginx.pid
COPY default.conf /etc/nginx/conf.d/default.conf
COPY supervisord.conf /etc/supervisord.conf
ADD ldap-client.tar.gz /
RUN chmod 777 /ldap-client -R && sed -i 's/;clear_env/clear_env/' /etc/php7/php-fpm.d/www.conf
EXPOSE 80 443
WORKDIR /var/run
CMD ["/usr/bin/supervisord"]
