FROM openresty/openresty:alpine

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx.conf         /usr/local/openresty/nginx/conf/nginx.conf
COPY metrics.conf       /etc/nginx/conf.d
COPY lib/prometheus.lua /usr/local/openresty/luajit/lib