FROM        aerth/php:latest
MAINTAINER  aerth@sdf.org
# Composer dependency manager
ADD https://github.com/vrana/adminer/tarball/master /tmp/
# There has to be a better way.
RUN cd /tmp && mv master master.tar.gz && gunzip -f master.tar.gz && tar -x -f master.tar && mv $(tar -t -f master.tar | head -n 1) adminer-source
RUN cd /tmp/adminer-source && php compile.php && mv adminer.php /var/www/public/adminer.php && cp -R /tmp/adminer-source/plugins /var/www/public/plugins
ADD ./src/index.php /var/www/public/index.php
EXPOSE 80
RUN chown -R nginx:nginx /var/www
CMD ["/run.sh"]
