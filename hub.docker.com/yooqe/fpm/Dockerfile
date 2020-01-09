FROM yooqe/php

ENV DEBIAN_FRONTEND noninteractive

RUN aptitude update -y
RUN aptitude install -y php5-fpm php5-apcu

ADD www.conf /etc/php5/fpm/pool.d/www.conf
ADD php.ini  /etc/php5/fpm/php.ini

EXPOSE 9000

ENTRYPOINT ["/usr/sbin/php5-fpm"]
CMD ["-F", "-R"]
