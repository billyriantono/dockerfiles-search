FROM nginx:1.14.0

RUN usermod -u 82 www-data
RUN groupmod -g 82 www-data

COPY nginx.conf /etc/nginx/nginx.conf
