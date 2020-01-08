FROM debian:latest

MAINTAINER veto@myridia.com

RUN apt-get update 
RUN apt-get remove --purge exim4 -y 

RUN apt-get install -y \
  apache2 \
  php7.0 \
  libapache2-mod-php7.0 \
  php7.0-json \
  php7.0-xml \
  php7.0-xmlrpc \
  php7.0-cgi  \
  php7.0-mbstring \
  php7.0-gd \
  php7.0-curl \
  php7.0-zip \
  php-redis \
  curl \
  emacs25-nox \ 
  apt-utils \
  php7.0-mcrypt \
  php7.0-curl \
  php7.0-redis \
  postgresql-client \
  postgresql-contrib \
  pgadmin3 \
  libdbd-pg-perl \
  texlive \
  php7.0-pgsql \
  ssmtp \
  supervisor \
  git


RUN rm /var/www/html -Rf
RUN git clone https://github.com/Tekki/sql-ledger.git /var/www/html

RUN echo "<?php phpinfo() ?>" > /var/www/html/index.php ; \
mkdir -p /var/lock/apache2 /var/run/apache2 /var/run/sshd /var/log/supervisor ; \
a2enmod rewrite cgi ;\

sed -i -e '/memory_limit =/ s/= .*/= 2056M/' /etc/php/7.0/apache2/php.ini ; \
sed -i -e '/post_max_size =/ s/= .*/= 800M/' /etc/php/7.0/apache2/php.ini ; \
sed -i -e '/max_file_uploads =/ s/= .*/= 200/' /etc/php/7.0/apache2/php.ini ; \
sed -i -e '/upload_max_filesize =/ s/= .*/= 800M/' /etc/php/7.0/apache2/php.ini ; \
sed -i -e '/display_errors =/ s/= .*/= ON/' /etc/php/7.0/apache2/php.ini ; \
sed -i -e '/short_open_tag =/ s/= .*/= ON/' /etc/php/7.0/apache2/php.ini ; \
sed -i -e '/short_open_tag =/ s/= .*/= ON/' /etc/php/7.0/cli/php.ini ; \
sed -i -e '/AllowOverride / s/ .*/ All/' /etc/apache2/apache2.conf ;


COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY sqlledger.conf /etc/apache2/sites-enabled/
COPY sql-ledger.conf /var/www/html

RUN usermod -c "Accounting" www-data
RUN usermod -c "Accounting" root


EXPOSE 80
CMD ["/usr/bin/supervisord"]
