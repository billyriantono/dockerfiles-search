FROM wordpress:latest

#RUN echo 'deb http://mirrors.163.com/debian/ jessie main non-free contrib'>/etc/apt/sources.list
#RUN echo 'deb http://mirrors.163.com/debian/ jessie-updates main non-free contrib'>>/etc/apt/sources.list
#RUN echo 'deb http://mirrors.163.com/debian/ jessie-backports main non-free contrib'>>/etc/apt/sources.list
#RUN echo 'deb-src http://mirrors.163.com/debian/ jessie main non-free contrib'>>/etc/apt/sources.list
#RUN echo 'deb-src http://mirrors.163.com/debian/ jessie-updates main non-free contrib'>>/etc/apt/sources.list
#RUN echo 'deb-src http://mirrors.163.com/debian/ jessie-backports main non-free contrib'>>/etc/apt/sources.list
#RUN echo 'deb http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib'>>/etc/apt/sources.list
#RUN echo 'deb-src http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib'>>/etc/apt/sources.list
RUN apt-get update && apt-get install -y unzip  && rm -r /var/lib/apt/lists/*

RUN touch /usr/local/etc/php/conf.d/upload-limit.ini \
    && echo "upload_max_filesize = 32M" >>/usr/local/etc/php/conf.d/upload-limit.ini \
    && echo "post_max_size = 32M" >>      /usr/local/etc/php/conf.d/upload-limit.ini

RUN a2enmod rewrite expires headers

VOLUME /var/www/html

COPY docker-entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["apache2-foreground"]
