FROM nginx:latest

ENV websiteloc /var/www/html
ENV nginx_conf /etc/nginx/conf.d/default.conf

COPY website ${websiteloc}
COPY nginx.conf ${nginx_conf}

EXPOSE 80
