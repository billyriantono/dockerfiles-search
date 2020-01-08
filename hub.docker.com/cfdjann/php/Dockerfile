FROM cfdjann/base
MAINTAINER JSK

# Install php5-fpm and nginx
RUN apt-get -y install php5-fpm php5-mysql php-apc php5-imagick php5-imap php5-mcrypt nginx sed
RUN apt-get clean

ADD ./default-site /etc/nginx/sites-available/default
RUN echo "cgi.fix_pathinfo = 0;" >> /etc/php5/fpm/php.ini
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log


RUN mkdir /webapp
RUN echo "<?php phpinfo(); ?>" > /webapp/index.php

ONBUILD RUN chown -R www-data:www-data /webapp
ONBUILD RUN chmod 775 /webapp

EXPOSE 80

CMD /etc/init.d/php5-fpm start && nginx