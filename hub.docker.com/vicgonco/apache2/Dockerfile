FROM debian:jessie

MAINTAINER Víctor González <victor.gonzalez@geomati.co>

ENV DEBIAN_FRONTEND noninteractive

RUN echo "deb http://httpredir.debian.org/debian jessie contrib" >> /etc/apt/sources.list
RUN set -x \
	&& apt-get update \
	&& apt-get install -yq apache2 \
  && rm -rf /var/lib/apt/lists/*

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2

ENTRYPOINT [ "/usr/sbin/apache2ctl", "-DFOREGROUND" ]

EXPOSE 80

