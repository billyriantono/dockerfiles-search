FROM nginx:alpine

RUN addgroup -g 500 symfony \
    && adduser -u 500 -D -G symfony -h /home/symfony -s /bin/sh symfony \
    && mkdir /srv/symfony \
    && chown symfony:symfony /srv/symfony

RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

ADD nginx.conf /etc/nginx/
ADD symfony.conf /etc/nginx/conf.d/

ADD entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod 0755 /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]

WORKDIR /srv/symfony