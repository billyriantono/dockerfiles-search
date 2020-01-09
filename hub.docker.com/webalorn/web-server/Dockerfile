FROM ubuntu
MAINTAINER webalorn <webalorn@gmail.com>

RUN apt-get update && \
	apt-get install -y apache2 php libapache2-mod-php php-mysql

RUN apt-get install -y libgmp-dev php7.0-gmp \
		curl php-curl \
		php-mbstring \
		php-xml \
		php-intl

RUN a2enmod rewrite headers && \
 	rm -R /etc/apache2/sites-enabled && \
 	mkdir /etc/apache2/sites-enabled

COPY root_files /

WORKDIR /data
EXPOSE 80

ENTRYPOINT ["server-entrypoint"]
CMD ["apache2-foreground"]