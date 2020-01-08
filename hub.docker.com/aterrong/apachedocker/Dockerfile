FROM ubuntu

# File Author / Maintainer
MAINTAINER aterrong

# Update the repository sources list

# Install and run apache
RUN apt-get update && apt-get install -y apache2 \
	&& sed -i "s:ErrorLog.*:ErrorLog /dev/stderr:g" /etc/apache2/sites-enabled/000-default.conf \
	&& sed -i "s:CustomLog.*:CustomLog /dev/stdout combined:g" /etc/apache2/sites-enabled/000-default.conf \
	&& apt-get clean

#ENTRYPOINT ["/usr/sbin/apache2", "-k", "start"]


#ENV APACHE_RUN_USER www-data
#ENV APACHE_RUN_GROUP www-data
#ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80
CMD apachectl -D FOREGROUND
