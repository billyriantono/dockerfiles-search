FROM openresty/openresty:alpine

ENV CONFIG="/opt/verynginx/verynginx/configs"

COPY ./verynginx /opt/verynginx/verynginx
COPY ./nginx.conf /usr/local/openresty/nginx/conf/nginx.conf
RUN mkdir -p "$CONFIG" && chmod -R 777 "$CONFIG"