FROM library/debian:stretch
MAINTAINER pau.curria@zitrogames.com

RUN	apt-get update && \
	apt-get -y install apache2 php php-mysql && \
	rm -rf /var/lib/dpkg /var/lib/apt /var/cache/apt /var/www/html/index.html && \
	ln -sf /dev/stdout /var/log/apache2/access.log && \
	ln -sf /dev/stderr /var/log/apache2/error.log

COPY index.html /var/www/html

ENTRYPOINT [ "/usr/sbin/apache2ctl", "-D", "FOREGROUND" ]
#CMD [ "8.8.8.8" ]
