FROM nginx:1.13.0-alpine

VOLUME /var/www/html
WORKDIR /var/www/html

ENV WORDPRESS_VERSION 5.2.2
ENV WORDPRESS_SHA1 65913a39b2e8990ece54efbfa8966fc175085794

RUN apk add --update curl tar;

RUN set -x \
	&& addgroup -g 82 -S www-data \
	&& adduser -u 82 -D -S -G www-data www-data \
	&& curl -o wordpress.tar.gz -fSL "https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz" \
    && tar -xzf wordpress.tar.gz -C / \
    && rm wordpress.tar.gz


EXPOSE 80
EXPOSE 443

STOPSIGNAL SIGQUIT

COPY entrypoint /usr/local/bin/entrypoint
COPY wp-config.php /wp-config.php

RUN chmod 777 /usr/local/bin/entrypoint
CMD ["entrypoint"]

#CMD ["nginx", "-g", "daemon off;"]