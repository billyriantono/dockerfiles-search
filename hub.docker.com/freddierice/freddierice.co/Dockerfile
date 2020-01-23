############################################################
# Dockerfile to build an apache image for freddierice.co
# Based on freddierice/freddierice.co (debian)
############################################################
FROM freddierice/freddierice.co
MAINTAINER Freddie Rice

RUN mkdir /root/utils \
	&& mkdir /root/domains \
	&& rm -rf /etc/apache2/sites-enabled/* /var/www/* \
	&& mkdir /var/www/static \ 
	&& chown -R www-data:www-data /var/www/static \ 
	&& chmod -R 755 /var/www/static 

COPY apache/ /etc/apache2
COPY domains/ /root/domains

COPY utils/ /root/utils
WORKDIR /root/utils
RUN gcc -O2 user_poweroff.c -o user_poweroff \
	&& rm -f ./user_poweroff.c \
	&& mv user_poweroff /usr/local/bin \
	&& chown root:root /usr/local/bin/user_poweroff \
	&& chmod 755 /usr/local/bin/user_poweroff \
	&& chmod u+s /usr/local/bin/user_poweroff 

WORKDIR /root/domains/www
RUN hugo \
	&& mkdir -p /var/www/www \
	&& chown -R www-data:www-data /var/www/www 

WORKDIR /root/domains/
RUN cp -r ./pulse /var/www/pulse \
	&& chown -R www-data:www-data /var/www/pulse

EXPOSE 80
ENTRYPOINT ["dumb-init", "apache2ctl", "-D", "FOREGROUND"]
