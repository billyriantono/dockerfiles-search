FROM debian:stretch
MAINTAINER GreenBiz
RUN apt-get update
RUN apt-get install -y apache2
RUN apt-get install -y \
  wget \
  php7.0 \
  php7.0-mysql \
  php7.0-ldap \
  php7.0-xmlrpc \
  curl \
  php7.0-curl \
  php7.0-gd \
  php7.0-mbstring \
  php7.0-simplexml \
  php7.0-imap \
  php7.0-apcu
RUN a2enmod rewrite && service apache2 stop
WORKDIR /var/www/html
COPY start.sh /opt/
RUN chmod +x /opt/start.sh
RUN usermod -u 1000 www-data
CMD /opt/start.sh
EXPOSE 80
