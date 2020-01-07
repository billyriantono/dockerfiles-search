FROM jschnabel/nginx:latest

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="jschnabel/nginx-php7" \
      org.label-schema.description="Lightweight Nginx container with php7" \
      org.label-schema.url="https://joshua-schnabel.de" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/joshua-schnabel/docker-nginx-php7/" \
      org.label-schema.vendor="Joshua Schnabel" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0" \
      Maintainer="Joshua Schnabel <dev@joshua-schnabel.de>" \
      Description="Lightweight Nginx container with php7."
      
ENV PHPVERSION="7.3.11-r0"

RUN bash -c "apk --no-cache add 'php7~=$PHPVERSION' 'php7-fpm~=$PHPVERSION' 'php7-mysqli~=$PHPVERSION' 'php7-json~=$PHPVERSION' \
            'php7-openssl~=$PHPVERSION' 'php7-curl~=$PHPVERSION' 'php7-zip~=$PHPVERSION' 'php7-xml~=$PHPVERSION' \
            'php7-phar~=$PHPVERSION' 'php7-intl~=$PHPVERSION' 'php7-dom~=$PHPVERSION' 'php7-xmlreader~=$PHPVERSION' \
            'php7-ctype~=$PHPVERSION' 'php7-session~=$PHPVERSION' 'php7-mbstring~=$PHPVERSION' 'php7-gd~=$PHPVERSION' 'php7-opcache~=$PHPVERSION'" && \
    rm -rf /var/cache/apk/* && \
    touch /etc/php-fpm.pid && \
    chown www-data:www-data /etc/php-fpm.pid && \
    chmod 644 /etc/php-fpm.pid && \
	mkdir -p /run/php/ && \
	chown www-data:www-data /run/php/
      
COPY ./CHANGELOG /CHANGELOG

COPY ./php/ /etc/php7/

COPY ./media /media/

COPY entrypoint-php.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint-php.sh
ENTRYPOINT ["entrypoint-php.sh"]

CMD ["nginx", "-g", "daemon off;"]
