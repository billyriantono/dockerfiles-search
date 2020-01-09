FROM ubuntu:16.04
MAINTAINER Hoang Nguyen <nbhoangit@gmail.com>
RUN apt-get update -y && \
	apt-get install -y \
	apache2 && \
	apt-get clean && \
	rm -rf \var\lib\lists\*

RUN a2enmod rewrite

RUN /usr/sbin/a2ensite default-ssl
RUN /usr/sbin/a2enmod ssl

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
