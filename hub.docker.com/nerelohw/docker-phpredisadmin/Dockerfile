FROM nerelohw/docker-php7
MAINTAINER Hongshun Yang<wholerencom@gmail.com>


ENV PHPREDISADMIN_VERSION 1.11.1
ENV PHPREDISADMIN_DOWNLOAD_URL https://github.com/erikdubbelboer/phpRedisAdmin/archive/v$PHPREDISADMIN_VERSION.tar.gz

RUN cd /root/ \ 
&& wget -qO- $PHPREDISADMIN_DOWNLOAD_URL | tar xvz \
&& mv phpRedisAdmin-$PHPREDISADMIN_VERSION phpredisadmin \
&& cd phpredisadmin \
&& composer update \
&& cd includes \
&& cp config.environment.inc.php config.inc.php \
&& sed -i ":begin; /array(/,/),/ { /)/! { $! { N; b begin };}; s/array(*.*127.*),/array(\n'servers'=>array(/;};" config.sample.inc.php

EXPOSE 80

WORKDIR "/root/phpredisadmin"

## https://github.com/erikdubbelboer/phpRedisAdmin/blob/master/includes/config.environment.inc.php

CMD ["php","-S","0.0.0.0:80"]
