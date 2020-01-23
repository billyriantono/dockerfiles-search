#Choose Debian
FROM debian:latest

MAINTAINER hadrian85 "hadrian85@web.de"

#Don't ask questions during install
ENV DEBIAN_FRONTEND noninteractive

#Install software
RUN apt update \
&& apt -y install \
apache2 \
supervisor \
python-certbot-apache \
nano

RUN a2enmod proxy \
&& a2enmod proxy_http \
&& a2enmod ssl \
&& a2enmod rewrite \
&& service apache2 stop

#Prepare proxy config
RUN rm -R /etc/letsencrypt \
&& ln -s /opt/reverseproxy/certs /etc/letsencrypt \
&& ln -s /opt/reverseproxy/reverseproxy.conf /etc/apache2/conf-enabled/reverseproxy.conf

#Supervisor
COPY supervisord.conf /etc/supervisor/supervisord.conf

#Ports
EXPOSE 80 443

#Volumes
VOLUME /opt/reverseproxy

ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisor/supervisord.conf"]