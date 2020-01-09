FROM nginx:1.16-alpine AS builder
WORKDIR /
RUN apk add --no-cache --virtual .build-deps \
    gcc \
    libc-dev \
    make \
    openssl-dev \
    pcre-dev \
    zlib-dev \
    linux-headers \
    curl \
    gnupg \
    libxslt-dev \
    gd-dev \
    geoip-dev \
    git && \
    wget 'http://nginx.org/download/nginx-1.16.1.tar.gz' && \
    tar -xzvf nginx-1.16.1.tar.gz && \
    cd nginx-1.16.1 && \
    git clone https://github.com/openresty/echo-nginx-module.git && \
    ./configure --add-dynamic-module=echo-nginx-module --with-perl_modules_path=/usr/lib/perl5/vendor_perl \
    --with-compat --with-file-aio --with-threads --with-http_addition_module --with-http_auth_request_module \
    --with-http_dav_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module \
    --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module \
    --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module \
    --with-http_v2_module --with-mail --with-mail_ssl_module --with-stream --with-stream_realip_module \
    --with-stream_ssl_module --with-stream_ssl_preread_module --with-cc-opt='-Os -fomit-frame-pointer' \
    --with-ld-opt=-Wl,--as-needed && \
    make -j2 && \
    make install
FROM nginx:1.16-alpine
COPY --from=builder /usr/local/nginx/modules/ngx_http_echo_module.so /usr/local/nginx/modules/ngx_http_echo_module.so
COPY conf/nginx.conf /etc/nginx/nginx.conf
COPY conf/default.conf /etc/nginx/conf.d/default.conf