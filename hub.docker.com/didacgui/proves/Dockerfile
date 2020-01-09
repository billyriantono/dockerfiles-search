FROM library/debian:stretch
MAINTAINER kenneth@floss.cat

RUN	apt-get update &&\
	apt-get -y install libapache2-mod-php7.0 php-mysql php-gd && \
	ln -sf /dev/stdout /var/log/apache2/access.log && \
	ln -sf /dev/sterr /var/log/apache2/error.log && \
	rm -rf /var/lib/dpg /var/lib/apt /var/cache/apt /var/www/html/index.html

ADD index.html /var/www/html/
ENTRYPOINT [ "/usr/sbin/apache2ctl", "-D", "FOREGROUND" ]
#CMD [ "8.8.8.8" ]
#EXPOSE 80


