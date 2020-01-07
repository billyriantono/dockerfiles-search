FROM debian:jessie

# add non free repository fock libapache2-mod-fascgi
RUN sed -i "s/jessie main/jessie main contrib non-free/" /etc/apt/sources.list

RUN apt-get update \
        && apt-get install -y --no-install-recommends \
            apache2 \
            libapache2-mod-fastcgi

RUN a2enmod proxy
RUN a2enmod proxy_fcgi
RUN a2enmod rewrite
RUN a2enmod expires

COPY ./conf/sites-available/* /etc/apache2/sites-available/
COPY ./conf/apache2.conf /etc/apache2/apache2.conf

#RUN a2dissite 000-default
#RUN a2ensite proxypass-test

WORKDIR /var/www/html

EXPOSE 80
EXPOSE 443

COPY ./start.sh /
RUN chmod 755 /start.sh

CMD ["/bin/bash","/start.sh"]