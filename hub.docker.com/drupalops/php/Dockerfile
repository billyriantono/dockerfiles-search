FROM drupalops/nginx

MAINTAINER Steve Oliver "https://github.com/steveoliver"

RUN apt-get update

RUN apt-get -y install php5-cli php5-mysql php5-curl php5 php5-fpm php5-gd php5-common php-pear curl php5-json php5-memcache

RUN echo "[PHP]\ncgi.fix_pathinfo = 0\ndispay_errors = On\n" >> /etc/php5/fpm/php.ini
RUN echo "[PHP]\nmax_execution_time = 600\n" >> /etc/php5/fpm/php.ini
RUN echo "[global]\ndaemonize = no\n[www]\nlisten.mode = '0660'\n" >> /etc/php5/fpm/php-fpm.conf
RUN echo "<?php print phpinfo(); ?>" > /srv/www/phpinfo.php

ADD php5-fpm.sv.conf /etc/supervisor/conf.d/php5-fpm.sv.conf

# Overwrites default nginx site definition from base drupalops/nginx image.
ADD ./default /etc/nginx/sites-available/default
