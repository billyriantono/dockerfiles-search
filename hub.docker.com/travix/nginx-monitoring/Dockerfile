FROM travix/base-alpine:3.4

MAINTAINER Travix

ENV OPENRESTY_VERSION=1.9.15.1

RUN apk add --update --no-cache --virtual build-deps \
    make gcc musl-dev pcre-dev openssl-dev zlib-dev ncurses-dev readline-dev curl perl \
 && mkdir -p /tmp/ngx_openresty \
 && cd /tmp/ngx_openresty \
 && curl -sSL http://openresty.org/download/openresty-${OPENRESTY_VERSION}.tar.gz | tar -xvz \
 && cd openresty-* \
 && ./configure \
    --prefix=/usr/share/nginx \
    --sbin-path=/usr/sbin/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=stderr \
    --http-log-path=/dev/stdout \
    --pid-path=/var/run/nginx.pid \
    --lock-path=/var/run/nginx.lock \
    --http-client-body-temp-path=/var/cache/nginx/client_temp \
    --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
    --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
    --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
    --http-scgi-temp-path=/var/cache/nginx/scgi_temp \
    --user=nginx \
    --group=nginx \
    --with-ipv6 \
    --with-luajit \
    --with-pcre-jit \
    --with-http_ssl_module \
    --without-http_ssi_module \
    --without-http_userid_module \
    --without-http_uwsgi_module \
    --without-http_scgi_module \
 && make \
 && make install \
 && ln -sf /usr/sbin/nginx /usr/local/bin/nginx \
 && ln -sf /usr/sbin/nginx /usr/local/bin/openresty \
 && ln -sf /usr/share/nginx/bin/resty /usr/local/bin/resty \
 && ln -sf /usr/share/nginx/luajit/bin/luajit-* /usr/share/nginx/luajit/bin/lua \
 && ln -sf /usr/share/nginx/luajit/bin/luajit-* /usr/local/bin/lua \
 && apk del build-deps \
 && apk add \
    libpcrecpp libpcre16 libpcre32 openssl libssl1.0 pcre libgcc libstdc++ \
 && rm -rf /var/cache/apk/* \
 && rm -rf /tmp/ngx_openresty \
 && mkdir -p \
    /usr/share/nginx/www \
    /var/cache/nginx/client_temp

WORKDIR /etc/nginx

# Add files
COPY config/ /etc/nginx/
COPY lua-modules/ /lua-modules

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]

# Expose on port 80 and 9090
EXPOSE 80 443 9090
