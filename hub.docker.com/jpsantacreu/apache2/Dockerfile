FROM library/debian:stretch
MAINTAINER juanpablo.santacreu@gmail.com
RUN apt-get update && \
	apt-get	-y install apache2 && \
	sed -i "s:ErrorLog.*:ErrorLog /dev/stderr:g" /etc/apache2/sites-available/000-default.conf && \
	sed -i "s:CustomLog.*:CustomLog /dev/stdout combined:g" /etc/apache2/sites-available/000-default.conf
EXPOSE 80
CMD [ "/usr/sbin/apachectl", "-D", "FOREGROUND" ]
ENTRYPOINT [ "/bin/bash" ] 
