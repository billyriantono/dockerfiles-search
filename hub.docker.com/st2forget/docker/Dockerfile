FROM node
MAINTAINER Gia, Le Huu Hoang <hoanggia.lh@gmail.com>

ENV TERM xterm
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y apache2 php5-mysql
RUN apt-get install -y php5 libapache2-mod-php5 php5-mcrypt
RUN apt-get install -y openssh-server supervisor

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN apt-get install -y nano
RUN apt-get install -y sudo
RUN apt-get install -y memcached php5-memcached php5-memcache
RUN apt-get install -y php-pear
RUN apt-get install -y build-essential
RUN apt-get install -y software-properties-common
RUN apt-get install -y libossp-uuid16
RUN apt-get install -y php5-cgi php5-cli php5-fpm
RUN apt-get install -y php5-dev libpcre3-dev uuid uuid-dev
RUN printf "\n" | pecl install uuid

# RUN add-apt-repository ppa:vbernat/haproxy-1.5
# RUN apt-get update -y && apt-get dist-upgrade -y
RUN apt-get install -y haproxy
RUN apt-get install -y php5-redis
RUN apt-get install -y libapache2-mod-xsendfile 

RUN apt-get install -y gearman-job-server libgearman-dev
RUN printf "\n" | pecl install gearman
RUN apt-get install -y curl libcurl3 libcurl3-dev
RUN apt-get install -y php5-curl
RUN apt-get install -y redis-tools

RUN a2enmod rewrite
RUN a2enmod xsendfile
RUN a2enmod headers

#uuid
RUN touch /etc/php5/mods-available/uuid.ini
RUN echo "extension=uuid.so" | tee /etc/php5/mods-available/uuid.ini
RUN cp /etc/php5/mods-available/uuid.ini /etc/php5/cli/conf.d/uuid.ini
RUN cp /etc/php5/mods-available/uuid.ini /etc/php5/apache2/conf.d/uuid.ini

#gearman
RUN touch /etc/php5/mods-available/gearman.ini
RUN echo "extension=gearman.so" | tee /etc/php5/mods-available/gearman.ini
RUN cp /etc/php5/mods-available/gearman.ini /etc/php5/cli/conf.d/gearman.ini
RUN cp /etc/php5/mods-available/gearman.ini /etc/php5/apache2/conf.d/gearman.ini
