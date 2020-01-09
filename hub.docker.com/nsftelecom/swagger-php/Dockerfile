FROM composer
WORKDIR /
RUN printf "#!/usr/bin/env sh\nexec /vendor/bin/swagger \$@" > /docker-entrypoint.sh
RUN chmod 755 /docker-entrypoint.sh
RUN echo "{}" > composer.json
RUN composer config repositories.packagist.org composer https://repo-eu-uk-1.packagist.org
RUN composer require zircote/swagger-php:2.0.13
ENTRYPOINT ["/docker-entrypoint.sh"]
WORKDIR /app
