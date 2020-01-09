FROM nginx:latest

COPY default.conf /etc/nginx/conf.d/
COPY index.html /usr/share/nginx/html/

RUN rm -rf /var/log/nginx/access.log /var/log/nginx/error.log
