FROM r1co/nginx

RUN apt-get update && apt-get install -y php5-fpm php5-mysql php5-gd

ADD supervisord/php.conf /etc/supervisor/conf.d/php.conf

# add upstream
ADD default.conf /etc/nginx/conf.d/default.conf
ADD www.conf /etc/php5/fpm/pool.d/www.conf

RUN echo "extension=gd.so" > /etc/php5/fpm/conf.d/20-gd.ini

RUN rm -r /app/template/etc/
RUN mkdir -p /app/template/etc/
RUN cp -r /etc/php5/ /app/template/etc
RUN cp -r /etc/nginx/ /app/template/etc


RUN echo "<?php phpinfo() ?>" > /usr/share/nginx/html/index.php

ENV CONFIG_TEMPLATES="/app/template/etc/nginx:/etc/nginx/#/app/template/etc/php5:/etc/php5/



