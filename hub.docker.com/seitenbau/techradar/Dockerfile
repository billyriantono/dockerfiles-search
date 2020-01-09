FROM nginx:1.16.0-alpine

COPY nginx/nginx.conf /etc/nginx/conf.d/techradar.template

COPY docs/index.html /var/www/techradar/index.html
COPY docs/radar.css /var/www/techradar/radar.css
COPY docs/radar.js /var/www/techradar/radar.js

VOLUME /var/www/techradar/config

EXPOSE 80

ENV NGINX_HOST="localhost"

CMD /bin/sh -c "envsubst < /etc/nginx/conf.d/techradar.template > /etc/nginx/conf.d/default.conf && exec nginx -g 'daemon off;'"