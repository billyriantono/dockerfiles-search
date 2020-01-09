FROM greenandbiz/php7_alpine
LABEL maintainer="Marc LEMARCHAND <Remade>"
RUN chown -R apache:apache /var/www
RUN sudo -u apache composer create-project --keep-vcs --prefer-dist laravel/laravel /tmp/www && cp -r /tmp/www/. /app/public/ && rm -r /tmp/www
RUN chown -R apache:apache /app && chmod -R 755 /app
RUN sed -i "s#DocumentRoot \"/app/public\"#DocumentRoot \"/app/public/public\"#g" /etc/apache2/httpd.conf \ 
    && sed -i "s#<Directory \"/app/public\">#<Directory \"/app/public/public\">#" /etc/apache2/httpd.conf

EXPOSE 80
EXPOSE 443

ADD docker-entrypoint.sh /root/docker-entrypoint.sh
ENTRYPOINT ["/root/docker-entrypoint.sh"]