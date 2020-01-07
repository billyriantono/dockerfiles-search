FROM nginx:mainline-alpine

COPY entrypoint.sh /entrypoint.sh
COPY nginx.conf /etc/nginx/nginx.conf
COPY nginx.vh.default.conf /etc/nginx/conf.d/default.conf

RUN apk add ca-certificates curl rsync \
 && chmod +x /entrypoint.sh \
 && chmod g+rwx /var/cache/nginx /var/run /var/log/nginx /etc/nginx/conf.d \
 && chgrp -R root /var/cache/nginx \
 && addgroup nginx root

CMD /entrypoint.sh
EXPOSE 8080
USER nginx
