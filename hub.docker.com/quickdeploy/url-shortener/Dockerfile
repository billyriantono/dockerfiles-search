FROM php:7.3-fpm

MAINTAINER Newnius <docker@newnius.com>

RUN curl -L https://github.com/newnius/short-link/archive/0.2.1.tar.gz > /tmp/shortlink.tar.gz \
	&& tar -C /tmp -xzvf /tmp/shortlink.tar.gz \
	&& mv /tmp/short-link-0.2.1/.htaccess /var/www/html \
	&& mv /tmp/short-link-0.2.1/* /var/www/html \
	&& rm -rf /tmp/*


ADD config/config.js /var/www/html/static/

ADD config/config.inc.php /var/www/html/

ADD bootstrap.sh /etc/

CMD /etc/bootstrap.sh