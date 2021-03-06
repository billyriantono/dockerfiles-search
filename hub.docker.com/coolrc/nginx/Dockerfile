FROM alpine:3.8

LABEL maintainer="https://github.com/coolrc136"


ENV NGINX_VERSION 1.15.10
ENV OPENSSL_VERSION OpenSSL_1_1_1b

RUN apk --no-cache add build-base git autoconf automake libtool wget tar zlib-dev pcre-dev pcre unzip jemalloc-dev patch linux-headers \
&& cd /tmp \
&& git clone https://github.com/bagder/libbrotli \
&& cd libbrotli \
&& ./autogen.sh \
&& ./configure \
&& make && make install\
&& cd  ../ \
&& echo "lobbrotli finished" \
&& git clone https://github.com/eustas/ngx_brotli.git \
&& cd ngx_brotli \
&& git submodule update --init \
&& cd ../ \
&& echo "ngx_brotli finished" \
&& wget -qO openssl.zip https://github.com/openssl/openssl/archive/${OPENSSL_VERSION}.zip \
&& unzip -q openssl.zip \
&& cd openssl-${OPENSSL_VERSION} \
&& wget -qO- https://raw.githubusercontent.com/hakasenyang/openssl-patch/master/openssl-equal-1.1.1b_ciphers.patch | patch -p1 \
&& cd ../ \
&& git clone https://github.com/openresty/headers-more-nginx-module.git \
&& wget  http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
&& tar zxf nginx-${NGINX_VERSION}.tar.gz \
&& cd nginx-${NGINX_VERSION} \
&& ./configure \
       --with-threads \
       --with-file-aio \
       --with-http_ssl_module \
       --with-http_v2_module \
       --with-http_gzip_static_module \
       --with-http_gunzip_module \
       --with-http_realip_module \
       --with-http_stub_status_module \
       --with-http_sub_module \
       --with-http_addition_module \
       --add-module=../ngx_brotli \
       --add-module=../headers-more-nginx-module \
       --with-openssl=../openssl-${OPENSSL_VERSION} \
       --with-openssl-opt='no-tests enable-ec_nistp_64_gcc_128 enable-tls1_3 -ljemalloc' \
       --with-ld-opt="-ljemalloc" \
       --with-cc-opt="-O3 -flto -fPIC -fPIE -fstack-protector-strong -Wformat -Werror=format-security -Wno-deprecated-declarations -Wno-strict-aliasing" \
&& echo "make start" \
&& make && make install \
&& echo "nginx finished" \
&& apk del build-base git autoconf automake libtool wget tar zlib-dev pcre-dev unzip jemalloc-dev patch linux-headers || true \
&& cd / && rm -rf /tmp/* \
&& ln -sf /usr/local/nginx/sbin/nginx /usr/sbin/nginx

#EXPOSE 80 443
CMD crond && /usr/local/nginx/sbin/nginx -g "daemon off;"

