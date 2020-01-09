FROM alpine:3.4
MAINTAINER Laoshancun <laoshancun@foxmail.com> 
ENV TENGINE_VERSION 2.2.0
ENV CONFIG "\    
    --prefix=/etc/nginx \
    --sbin-path=/usr/sbin/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --pid-path=/var/run/nginx.pid \
    --lock-path=/var/run/nginx.lock \
    --http-client-body-temp-path=/var/cache/nginx/client_temp \
    --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
    --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
    --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
    --http-scgi-temp-path=/var/cache/nginx/scgi_temp \
    --user=nginx \
    --group=nginx \
    --with-pcre \
    --add-module=deps/lua-nginx-module \
    --add-module=deps/ngx_devel_kit-0.2.19 \
    --with-http_upstream_check_module \
    --with-http_v2_module \
    --with-syslog \
    --with-http_ssl_module \
    --with-http_realip_module \
    --with-http_addition_module \
    --with-http_sub_module \
    --with-http_dav_module \
    --with-http_gunzip_module \
    --with-http_gzip_static_module \
    --with-http_secure_link_module \
    --with-http_auth_request_module \
    --with-file-aio \
    --with-ipv6 \
    --with-jemalloc \
    "
 
ADD nginx.patch /
ADD repositories /etc/apk/repositories

RUN \
  addgroup -S nginx \
  && adduser -D -S -h /var/cache/nginx -s /sbin/nologin -G nginx nginx \
  && apk add --no-cache --virtual .build-deps \
    gcc \
    libc-dev \
    make \
    openssl-dev \
    pcre-dev \
    zlib-dev \
    linux-headers \
    curl \
    jemalloc-dev \
    luajit-dev \
    lua5.1-dev \
  && curl "http://tengine.taobao.org/download/tengine-$TENGINE_VERSION.tar.gz" -o tengine.tar.gz \
  && curl "https://codeload.github.com/simpl/ngx_devel_kit/tar.gz/v0.2.19" -o ngx_devel_kit-v0.2.19.tar.gz \  
  && curl "https://codeload.github.com/openresty/lua-nginx-module/tar.gz/v0.10.6" -o lua-nginx-module-v0.10.6.tar.gz \  
  
  && mkdir -p /usr/src \
  && tar -zxC /usr/src -f tengine.tar.gz \
  && mkdir -p /usr/src/tengine-$TENGINE_VERSION/deps \
  && tar -zxC /usr/src/tengine-$TENGINE_VERSION/deps -f ngx_devel_kit-v0.2.19.tar.gz \
  && tar -zxC /usr/src/tengine-$TENGINE_VERSION/deps -f lua-nginx-module-v0.10.6.tar.gz \
  && mv /usr/src/tengine-$TENGINE_VERSION/deps/lua-nginx-module-0.10.6 /usr/src/tengine-$TENGINE_VERSION/deps/lua-nginx-module \ 
  && rm tengine.tar.gz \
  && rm ngx_devel_kit-v0.2.19.tar.gz \
  && rm lua-nginx-module-v0.10.6.tar.gz \
  && cd /usr/src/tengine-$TENGINE_VERSION/src/core/ \
  && mv /nginx.patch ./nginx.patch \
  && patch nginx.h nginx.patch \
  && rm nginx.patch \
  && cd ../../ \
  && ./configure $CONFIG --with-debug \
  && make \
  && mv objs/nginx objs/nginx-debug \
  && ./configure $CONFIG \
  && make \
  && make install \
  && rm -rf /etc/nginx/html/ \
  && mkdir -p /data/www/ \
  && install -m644 html/index.html /data/www/ \
  && install -m644 html/50x.html /data/www/ \
  && install -m755 objs/nginx-debug /usr/sbin/nginx-debug \
  && strip /usr/sbin/nginx* \
  && runDeps="$( \
    scanelf --needed --nobanner /usr/sbin/nginx \
      | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
      | sort -u \
      | xargs -r apk info --installed \
      | sort -u \
  )" \
  && apk add --virtual .nginx-rundeps $runDeps \
  && apk del .build-deps \
  && rm -rf /usr/src/nginx-$NGINX_VERSION \
  && apk add --no-cache gettext \
  # forward request and error logs to docker log collector
  && ln -sf /dev/stdout /var/log/nginx/access.log \
  && ln -sf /dev/stderr /var/log/nginx/error.log
 
#COPY nginx/* /etc/nginx/
 
EXPOSE 80 443
 
CMD ["nginx", "-g", "daemon off;"]
