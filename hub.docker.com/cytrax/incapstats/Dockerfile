# Dockerfile
FROM nimmis/apache-php5

MAINTAINER SemaphoreCI <dev@semaphoreci.com>

COPY / /etc/www/

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
