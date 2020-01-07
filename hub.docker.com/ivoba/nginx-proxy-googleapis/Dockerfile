FROM nginx:1.17-alpine

COPY nginx.conf /etc/nginx/nginx.conf

ARG PROXY

RUN sed -i "s@REPLACE_BY_ENV@$PROXY@g" /etc/nginx/nginx.conf
