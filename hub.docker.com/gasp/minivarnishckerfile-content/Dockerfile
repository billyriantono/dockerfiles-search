FROM nginx

ENV CONTAINER_NAME=nginx-proxy

RUN cat /etc/hosts

RUN rm /etc/nginx/conf.d/default.conf
COPY static /usr/share/nginx/html

COPY conf /etc/nginx/conf.d/