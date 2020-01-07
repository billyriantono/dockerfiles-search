FROM nginx:alpine
WORKDIR /etc/nginx

COPY nginx.conf .
COPY nginx-entrypoint.sh ./nginx-entrypoint.sh
COPY symfony.conf ./symfony.template.conf
RUN mkdir sites-available
RUN rm ./conf.d/default.conf
RUN echo "upstream php-upstream { server web:9000; }" > ./conf.d/upstream.conf
RUN adduser -D -u 1000 www-data

ENTRYPOINT ./nginx-entrypoint.sh

EXPOSE 80 443
