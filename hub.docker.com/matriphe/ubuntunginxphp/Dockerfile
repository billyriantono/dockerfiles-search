FROM phusion/baseimage:0.9.16
MAINTAINER Muhammad Zamroni <zam@nuwira.com>
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh
CMD ["/sbin/my_init"]
# Nginx-PHP Installation
RUN apt-get update && apt-get install -y wget nano curl build-essential software-properties-common
#RUN add-apt-repository -y ppa:ondrej/php5
RUN touch /etc/apt/sources.list.d/ondrej-php5.list
RUN echo "deb http://ppa.launchpad.net/ondrej/php5/ubuntu trusty main" >> /etc/apt/sources.list.d/ondrej-php5.list
RUN echo "deb-src http://ppa.launchpad.net/ondrej/php5/ubuntu trusty main" >> /etc/apt/sources.list.d/ondrej-php5.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C
RUN add-apt-repository -y ppa:nginx/stable
RUN apt-get update && apt-get install -y --force-yes php5-cli php5-fpm php5-mysql php5-pgsql php5-sqlite php5-curl php5-gd php5-imagick php5-mcrypt php5-intl php5-imap php5-tidy
RUN sed -i "s/;date.timezone =.*/date.timezone = Asia\/Jakarta/" /etc/php5/fpm/php.ini
RUN sed -i "s/;date.timezone =.*/date.timezone = Asia\/Jakarta/" /etc/php5/cli/php.ini
RUN php5enmod mcrypt
RUN apt-get install -y nginx
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php5/fpm/php.ini
RUN mkdir -p        /var/www/html
ADD build/default   /etc/nginx/sites-available/default
RUN mkdir           /etc/service/nginx
ADD build/nginx.sh  /etc/service/nginx/run
RUN chmod +x        /etc/service/nginx/run
RUN mkdir           /etc/service/phpfpm
ADD build/phpfpm.sh /etc/service/phpfpm/run
RUN chmod +x        /etc/service/phpfpm/run
ADD build/index.php /var/www/html/
RUN chmod +x        /var/www/html/index.php
EXPOSE 80
# End Nginx-PHP
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*