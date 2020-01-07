FROM nginx:1.10

MAINTAINER rdev02@outlook.com

COPY default.conf /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf

VOLUME /var/www/html
EXPOSE 80

ENTRYPOINT ["nginx"]