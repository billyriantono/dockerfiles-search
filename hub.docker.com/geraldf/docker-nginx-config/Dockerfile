FROM nginx:alpine

RUN rm -v /etc/nginx/conf.d/*
COPY config/nginx.conf /etc/nginx/nginx.conf
COPY config/portainer.conf /etc/nginx/conf.d/portainer.conf
