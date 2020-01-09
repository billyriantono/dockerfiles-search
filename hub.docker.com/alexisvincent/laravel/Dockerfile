#
# Laravel Dockerfile
#
# https://github.com/alexisvincent/Dockerfiles/laravel
#

FROM alexisvincent/nginx.hhvm:3.5.1
MAINTAINER Alexis Vincent "alexisjohnvincent@gmail.com"

# Add configs
COPY container/default.conf /etc/nginx/conf.d/default.conf
COPY container/index.php /data/www/index.php

# Container Config
CMD ["/usr/bin/supervisord"]
EXPOSE 80 443