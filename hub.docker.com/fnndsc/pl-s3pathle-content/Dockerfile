FROM php:7.3.3-apache-stretch

ENV PORT 5000

COPY ./app/* /var/www/html

COPY ./setApachePort.sh /

RUN chmod a+x /setApachePort.sh

CMD ["/setApachePort.sh"]
