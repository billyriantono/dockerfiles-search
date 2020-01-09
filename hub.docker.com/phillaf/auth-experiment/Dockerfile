FROM openresty/openresty:alpine-fat

RUN opm get SkyLothar/lua-resty-jwt && \
    luarocks install uuid

COPY ./conf /etc/nginx/conf.d
COPY ./nginx.conf /usr/local/openresty/nginx/conf/nginx.conf

EXPOSE 80
