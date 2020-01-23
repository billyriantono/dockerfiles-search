FROM ubuntu:16.04

ARG WEBDAV_REALM=webdav
ARG WEBDAV_USER=user
ARG WEBDAV_PW=secret

ENV DEBIAN_FRONTEND noninteractive
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_RUN_DIR /var/run/apache2

RUN apt-get update && \
	apt-get install -y \
		apache2 \
		apache2-utils \
		php \
		libapache2-mod-php \
		expect

COPY config/apache/000-default.conf /etc/apache2/sites-available/
COPY config/webdav/webdav.conf /etc/apache2/sites-available/
COPY config/webdav/htdig.exp .

RUN mkdir /var/www/webdav && \
	mkdir /var/www/webdav/atoms && \
	chown -R $APACHE_RUN_USER:$APACHE_RUN_GROUP /var/www && \
	a2enmod dav dav_fs && \
	./htdig.exp /etc/apache2/users.password $WEBDAV_REALM $WEBDAV_USER $WEBDAV_PW && \
	chown $APACHE_RUN_USER:$APACHE_RUN_GROUP /etc/apache2/users.password && \
	echo "ServerName localhost" | tee /etc/apache2/conf-available/fqdn.conf && \
	a2enmod auth_digest && \
	a2ensite webdav && \
	a2dissite 000-default && \
	a2enconf fqdn

EXPOSE 80

CMD apache2 -DFOREGROUND
