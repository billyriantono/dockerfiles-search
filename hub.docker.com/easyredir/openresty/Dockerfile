FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive
ENV OPENRESTY_VERSION 1.11.2.5
ENV OPENRESTY_PREFIX /usr/local/openresty

RUN apt-get update && apt-get install -y procps libpcre3 libssl1.0.0 libgeoip1 ca-certificates --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN buildDeps='curl perl make build-essential libreadline-dev libncurses5-dev libpcre3-dev libssl-dev libgeoip-dev' \
    && set -x \
    && apt-get update && apt-get install -y $buildDeps --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* \
    && curl -SL "https://openresty.org/download/openresty-${OPENRESTY_VERSION}.tar.gz" -o openresty.tar.gz \
    && mkdir -p /usr/src/openresty \
    && tar -xzf openresty.tar.gz -C /usr/src/openresty --strip-components=1 \
    && rm openresty.tar.gz \
    && cd /usr/src/openresty \
    && readonly NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && ./configure \
       --prefix=${OPENRESTY_PREFIX} \
       --sbin-path=/usr/sbin/nginx \
       --conf-path=/etc/nginx/nginx.conf \
       --lock-path=/var/lock/nginx.lock \
       --pid-path=/run/nginx.pid \
       --http-log-path=/var/log/nginx/access.log \
       --error-log-path=/var/log/nginx/error.log \
       --http-client-body-temp-path=/var/cache/nginx/client_temp \
       --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
       --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
       --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
       --http-scgi-temp-path=/var/cache/nginx/scgi_temp \
       --with-luajit \
       --with-stream \
       --with-stream_ssl_module \
       --with-http_geoip_module \
       --with-http_gzip_static_module \
       --with-http_realip_module \
       --with-http_stub_status_module \
       --with-http_ssl_module \
       --with-http_sub_module \
       --with-http_v2_module \
       --with-http_stub_status_module \
       --with-http_slice_module \
       --with-http_secure_link_module \
       --with-http_auth_request_module \
       --with-threads \
       --with-file-aio \
       --with-ipv6 \
       --with-pcre-jit \
       --without-lua_resty_mysql \
       --without-lua_resty_websocket \
       --with-cc-opt='-g -O2 -fstack-protector-strong -Wformat -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fPIC' \
       --with-ld-opt='-Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-z,now -Wl,--as-needed -pie' \   
       -j${NPROC} \
    && make -j${NPROC} \
    && make install \
    && mkdir -p /var/cache/nginx/client_temp && chmod 755 /var/cache/nginx/client_temp \
    && mkdir -p /var/cache/nginx/proxy_temp && chmod 755 /var/cache/nginx/proxy_temp \
    && mkdir -p /var/cache/nginx/fastcgi_temp && chmod 755 /var/cache/nginx/fastcgi_temp \
    && mkdir -p /var/cache/nginx/uwsgi_temp && chmod 755 /var/cache/nginx/uwsgi_temp \
    && mkdir -p /var/cache/nginx/scgi_temp && chmod 755 /var/cache/nginx/scgi_temp \
    && mkdir -p /etc/nginx/ssl && chmod 700 /etc/nginx/ssl \
    && cd / && rm -rf /usr/src/openresty \
    && apt-get purge -y --auto-remove $buildDeps

ADD dhparam2048.pem /etc/nginx/ssl/dhparam2048.pem
ADD dhparam4096.pem /etc/nginx/ssl/dhparam4096.pem

CMD ["nginx", "-g", "daemon off; error_log /dev/stderr info;"]
