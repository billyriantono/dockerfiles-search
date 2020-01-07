# Apache 2 with modsecurity

FROM debian:jessie

MAINTAINER geksiong@gmail.com

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_PID_FILE /var/run/apache2/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2

RUN \
  apt-get update && apt-get install -y \
    apache2 \
	libapache2-mod-security2 \
  && cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf \
  && a2enmod rewrite \
  && a2enmod headers \
  && a2enmod ssl \
  && a2enmod proxy \
  && a2enmod proxy_http \
  && a2enmod deflate \
  && a2enmod proxy_html \
  && a2enmod xml2enc \
  && cp /usr/share/zoneinfo/Asia/Singapore /etc/localtime \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

EXPOSE 80 443

VOLUME ["/etc/apache2/sites-enabled"]
VOLUME ["/etc/apache2/certs"]

ENTRYPOINT ["apache2", "-D", "FOREGROUND"]
