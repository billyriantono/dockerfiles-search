FROM stackd/php

WORKDIR /var/www
RUN rm -rf html/ && \
  apt-get update && \
  apt-get -y install git && \
  git clone --depth 1 https://github.com/phpmyadmin/phpmyadmin.git html
COPY config.inc.php /var/www/html/
