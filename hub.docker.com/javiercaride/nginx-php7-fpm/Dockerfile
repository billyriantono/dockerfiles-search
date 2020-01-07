FROM nginx
MAINTAINER Javier Caride "javier.caride@gmail.com"
ENV REFRESHED_AT 2017-03-14

ENV DEBIAN_FRONTEND noninteractive

# Upgrading the distribution and installing basic tools
RUN apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y net-tools wget curl sudo
 
# Adding dotdeb.org repository
RUN echo 'deb http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list \
  && echo 'deb-src http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list \
  && wget -qO - https://www.dotdeb.org/dotdeb.gpg | apt-key add - \
  && apt-get update

RUN apt-get install -y php7.0-fpm php7.0-cli php7.0-dev php7.0-bz2 php7.0-curl php7.0-gd php7.0-geoip php7.0-imagick php7.0-imap php7.0-intl php7.0-json php7.0-mbstring php7.0-mcrypt php7.0-memcached php7.0-mongodb php7.0-opcache php7.0-pspell php7.0-readline php7.0-recode php7.0-redis php7.0-soap php7.0-tidy php7.0-xdebug php7.0-xml php7.0-xmlrpc php7.0-xsl php7.0-zip php7.0-calendar php7.0-dom php7.0-exif php7.0-fileinfo php7.0-ftp php7.0-gettext php7.0-iconv php7.0-mysqli php7.0-mysqlnd php7.0-pdo php7.0-pdo-mysql php7.0-phar php7.0-posix php7.0-simplexml php7.0-shmop php7.0-sockets php7.0-sysvmsg php7.0-sysvshm

RUN sudo sed -i -e 's/www-data/nginx/g' /etc/php/7.0/fpm/pool.d/www.conf

COPY start-services.sh /usr/local/sbin
RUN chmod 700 /usr/local/sbin/start-services.sh

EXPOSE 80 443 9000

CMD ["/usr/local/sbin/start-services.sh"]
