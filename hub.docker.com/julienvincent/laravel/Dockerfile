# julienvincent/laravel:php

FROM julienvincent/nginx-hhvm:3.10.1
MAINTAINER Julien Vincent "julienlucvincent@gmail.com"

# Copy config
COPY container/default.conf /etc/nginx/conf.d/default.conf

VOLUME ["/data/www"]
EXPOSE 80 443