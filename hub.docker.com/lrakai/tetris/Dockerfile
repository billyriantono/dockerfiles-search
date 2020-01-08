FROM nginx:alpine

COPY www /www
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD (tail -F /var/log/nginx/access.log &) && sed -i "s/{{hostname}}/${hostname}/g" /www/index.html && exec nginx -g "daemon off;"
