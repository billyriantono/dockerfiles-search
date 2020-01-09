FROM library/debian:stretch
MAINTAINER edgardha@gmail.com

RUN	apt-get update && \
	apt-get install -y libapache2-mod-php7.0 apache2 php7.0 && \
	rm -rf /var/lib/dpkg /var/lib/apt /var/cache/apt /var/www/html/index.html &&\
	ln -sf /dev/stdout /var/log/apache2/access.log &&\
	ln -sf /dev/stderr /var/log/apache2/error.log

ENTRYPOINT [ "/usr/sbin/apache2ctl", "-D", "FOREGROUND" ]
COPY index.html /var/www/html
#CMD [ "8.8.8.8" ]
#EXPOSE	80

