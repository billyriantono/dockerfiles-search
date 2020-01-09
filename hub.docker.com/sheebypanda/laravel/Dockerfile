FROM eboraas/laravel:latest

#package update and install sqlite support for php
RUN apt-get update && apt-get -y install php5-sqlite  && apt-get -y dist-upgrade && apt-get -y autoremove && apt-get clean

#update composer
RUN /usr/local/bin/composer self-update


RUN mv /var/www/laravel /var/www/laravel_old

#install laravel
RUN /usr/local/bin/composer create-project laravel/laravel /var/www/laravel --prefer-source

#set proper files permissions
RUN /bin/chown www-data:www-data -R /var/www/laravel/

#open ports
EXPOSE 80
EXPOSE 443

#launch apache
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
