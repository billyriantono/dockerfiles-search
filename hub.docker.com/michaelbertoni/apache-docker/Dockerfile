FROM debian:8.8

RUN sed -i 's/main/main non-free/g' /etc/apt/sources.list

RUN \ 
	apt-get update \
	&& apt-get install -y wget bzip2 curl

RUN apt-get install -y --no-install-recommends apache2

COPY nextcloud.conf /etc/apache2/sites-available/nextcloud.conf

RUN \
	a2enmod proxy_fcgi rewrite headers env dir mime setenvif \
	&& a2ensite nextcloud

COPY nextcloud.sh /tmp/nextcloud.sh

RUN bash /tmp/nextcloud.sh

# https://github.com/Yelp/dumb-init
RUN curl -fLsS -o /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 && chmod +x /usr/local/bin/dumb-init

EXPOSE 80
EXPOSE 443

ENTRYPOINT ["/usr/local/bin/dumb-init", "--"]

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
