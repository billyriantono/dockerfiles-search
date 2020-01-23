ARG VERSION=latest
ARG PHP=latest

FROM wordpress:$VERSION AS wp

FROM wordpress:cli-2.4 AS wp-cli

FROM gendall/php:$PHP

ENV WP_DEBUG=true WP_DEBUG_DISPLAY=false WP_DEBUG_LOG=true \
    WORDPRESS_DB_HOST=db WORDPRESS_DB_USER=wordpress WORDPRESS_DB_PORT=3306 \
    SITE_NAME=Default

# add packages
RUN apt-get update && apt-get install -y sudo less mysql-client

# add wordpress and cli
COPY --from=wp /usr/src/wordpress /usr/src/wordpress
COPY --from=wp /usr/local/bin/docker-entrypoint.sh /usr/local/bin/wp-entrypoint.sh
COPY --from=wp-cli /usr/local/bin/wp /usr/local/bin/wp-cli
COPY wp-su.sh /usr/local/bin/wp

WORKDIR /var/www/html/wp-content

RUN mv /usr/local/bin/docker-entrypoint.sh /usr/local/bin/php-entrypoint.sh
COPY entrypoint.sh /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]
