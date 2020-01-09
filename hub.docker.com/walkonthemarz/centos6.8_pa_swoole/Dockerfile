#FROM centos:6.8
#FROM walkonthemarz/pa_base:latest
FROM walkonthemarz/pa_reader:latest

MAINTAINER walkonthemarz@gmail.com

COPY supervisord.conf /etc/supervisord.conf
    
COPY php.ini /etc/php.ini

COPY swoole /swoole

HEALTHCHECK --interval=5s --timeout=3s CMD curl -fs http://localhost || exit 1
EXPOSE 80
CMD []
#ENTRYPOINT ["/opt/rh/httpd24/root/usr/sbin/apachectl", "-D", "FOREGROUND"]
ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
