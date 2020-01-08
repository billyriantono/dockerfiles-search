FROM orukami/alpine-php:5.6

ENV WWW_ROOT /srv/www
ENV PUBLIC_ROOT /srv/www/public

COPY nginx /etc/nginx
COPY fpm /etc/php/fpm
COPY supervisord.conf /etc/supervisord.conf
COPY entrypoint.sh /

RUN apk add -U nginx supervisor && \
    mkdir -p /srv && mkdir -p ${WWW_ROOT} && \
    rm -rf /var/cache/apk/* && \
    chmod +x /entrypoint.sh

WORKDIR ${WWW_ROOT}

EXPOSE 80 443

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/usr/bin/supervisord"]
