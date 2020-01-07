FROM openresty/openresty:alpine-fat
RUN apk add --no-cache openssl-dev
RUN apk add --no-cache git
RUN luarocks install lapis

VOLUME /app
WORKDIR /app

EXPOSE 8080

ENTRYPOINT ["/usr/local/openresty/luajit/bin/lapis"]
CMD ["server", "production"]