FROM mrecco/nginx:latest

COPY ./config /nginx/conf

RUN /bin/bash -c "                                                          \
   mkdir -p /var/lib/nginx/cache/all /var/lib/nginx/cache/fpm /nginx/ssl && \
   chown -R www-data /var/lib/nginx/cache/all /var/lib/nginx/cache/fpm   && \
   chmod 700 /var/lib/nginx/cache/all /var/lib/nginx/cache/fpm"

EXPOSE 1000

ENTRYPOINT ["nginx", "-c", "/nginx/conf/nginx.conf", "-g", "daemon off;"]
