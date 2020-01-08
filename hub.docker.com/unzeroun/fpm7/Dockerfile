FROM unzeroun/php7

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y php7.0-fpm

ADD www.conf /etc/php/7.0/fpm/pool.d/www.conf
ADD php.ini  /etc/php/7.0/fpm/php.ini

EXPOSE 9000

ENTRYPOINT ["/usr/sbin/php-fpm7.0"]
CMD ["-F", "-R"]

