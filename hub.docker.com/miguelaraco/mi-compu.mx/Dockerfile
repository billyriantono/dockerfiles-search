FROM miguelaraco/alpine-nginx-php

RUN apk add --update \
	php7-xml \
	php7-ctype && \
	rm -rf /var/cache/apk/*

RUN rm /var/www/html/index.php

COPY src /var/www/html