FROM nginx
RUN mkdir -p var/www/html/static
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/nginx.conf