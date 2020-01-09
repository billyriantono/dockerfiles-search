FROM alpine:3.9.3

COPY CyberChef/ /www

RUN addgroup www -S && \
    adduser www -G www -S && \
    apk update && \
    apk add nginx && \
    rm -rf /var/cache/apk/*

RUN chown -R www:www /var/lib/nginx && \
    chown -R www:www /www && \
    mkdir -p /run/nginx && \
    chown -R www:www /run/nginx && \
    rm -rf /var/cache/apk/* && \
    mv /www/CyberChef_v9.7.1.html /www/index.html

COPY ./resources/nginx.conf /etc/nginx/nginx.conf

USER www
EXPOSE 8000
ENTRYPOINT ["nginx", "-c", "/etc/nginx/nginx.conf", "-g", "daemon off;"]