FROM fedora:29
LABEL version="0.5"

EXPOSE 80/tcp
EXPOSE 443/tcp

RUN  dnf -y update && \
     dnf -y install httpd php-fpm mod_ssl && \
     dnf clean all

COPY conf/php.conf /etc/httpd/conf.d/php.conf
COPY conf/httpd.conf /etc/httpd/conf/httpd.conf
COPY conf/ssl.conf /etc/httpd/conf.d/ssl.conf

VOLUME /etc/httpd/vhosts
VOLUME /etc/httpd/certs
VOLUME /var/www/html

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
