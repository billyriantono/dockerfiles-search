FROM merorafael/php-apache
 
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod proxy
RUN a2enmod proxy_http

WORKDIR /opt

RUN apt-get update && apt-get install -y \
	git \
	cron

RUN git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt --depth=1

RUN wget -O -  https://get.acme.sh | sh

RUN apache2ctl -D BACKGROUND

EXPOSE 8080 443

CMD ["apache2ctl", "-D", "FOREGROUND"]
