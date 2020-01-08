FROM alpine:3.7

LABEL maintainer="hgati <cobays@gmail.com>"

ENV TZ Asia/Seoul
ENV NGINX_VERSION 1.14.0
ENV GEOIP_VERSION 1.6.11
ENV ECHO_VERSION 0.61

# language 정적모듈컴파일방법: --add-module=<경로명>
# language 동적모듈컴파일방법: --add-dynamic-module=<경로명>
# https://www.nginx.com/resources/wiki/extending/converting/#compiling-a-dynamic-module
# https://www.nginx.com/resources/wiki/modules/accept_language/#accept-language-installation
# https://www.nginx.com/blog/compiling-dynamic-modules-nginx-plus/
# 정적모듈컴파일방식(옛날 config파일포맷임): http://www.nginxguts.com/2011/01/plugs/
# wget ssl지원: https://asciinema.org/a/101395
# CONFiG에 지정할 디렉토리 경로명: /tmp/nginx_accept_language_module-master
# echo-nginx-module-0.61

RUN set -x \
    && echo "==================================================" \
    && echo "Installing build environment" \
    && echo "==================================================" \
    && apk --update add --no-cache --virtual .build-deps \
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
    && runtime_packages="openssl pcre zlib libgcc" \
    && apk add ${runtime_packages} \
    && echo "==================================================" \
    && echo "Installing timezone (tzdata)" \
    && echo "==================================================" \
    && apk add --update --no-cache tzdata \
    && echo "==================================================" \
    && echo "Downloading echo-nginx-module" \
    && echo "==================================================" \
    && wget https://github.com/openresty/echo-nginx-module/archive/v${ECHO_VERSION}.tar.gz \
        -O /tmp/echo-nginx-module.tar.gz \
    && cd /tmp && tar -xvzf echo-nginx-module.tar.gz \
    && mv echo-nginx-module-${ECHO_VERSION} echo-nginx-module \
    && echo "==================================================" \
    && echo "Downloading nginx_accept_language_module" \
    && echo "==================================================" \
    && wget https://github.com/giom/nginx_accept_language_module/archive/master.zip \
        -O /tmp/nginx_accept_language_module.zip \
    && echo "- 만약 동적모듈로서 설치하고싶으면, 아래주소에서 다운로드하세요 !" \
    && echo "- wget -P /tmp/ https://github.com/hgati/nginx_accept_language_module/archive/master.zip" \
    && cd /tmp && unzip /tmp/nginx_accept_language_module.zip \
    && mv nginx_accept_language_module-* nginx_accept_language_module \
    && echo "==================================================" \
    && echo "Installing geoip-api-c" \
    && echo "==================================================" \
    && wget https://github.com/maxmind/geoip-api-c/releases/download/v${GEOIP_VERSION}/GeoIP-${GEOIP_VERSION}.tar.gz \
        -O /tmp/GeoIP.tar.gz \
    && cd /tmp && tar -xvzf GeoIP.tar.gz && mv GeoIP-* GeoIP \
    && cd GeoIP \
    && ./configure --prefix=/usr \
    && make -j$(getconf _NPROCESSORS_ONLN) \
    && make check \
    && make install \
    && echo "==================================================" \
    && echo "Downloading GeoIP database" \
    && echo "==================================================" \
    && mkdir /usr/share/GeoIP && cd /tmp \
    && wget http://geolite.maxmind.com/download/geoip/database/GeoLiteCountry/GeoIP.dat.gz \
    && gunzip GeoIP.dat.gz \
    && wget http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz \
    && gunzip GeoLiteCity.dat.gz \
    && mv GeoIP.dat GeoLiteCity.dat /usr/share/GeoIP/ \
    && echo "==================================================" \
    && echo "Downloading ngx_cache_purge" \
    && echo "==================================================" \
    && wget https://github.com/FRiCKLE/ngx_cache_purge/archive/2.3.tar.gz -O /tmp/ngx_cache_purge.tar.gz \
    && cd /tmp && tar -xvzf ngx_cache_purge.tar.gz && mv ngx_cache_purge-* ngx_cache_purge \
    && echo "==================================================" \
    && echo "Installing LuaJIT" \
    && echo "==================================================" \
    && wget http://luajit.org/download/LuaJIT-2.0.5.tar.gz -O /tmp/LuaJIT.tar.gz \
    && cd /tmp && tar -xvzf LuaJIT.tar.gz && mv LuaJIT-* LuaJIT && cd LuaJIT && make && make install \
    && echo "- LuaJIT 2.0 찾을곳을 nginx의 빌드시스템에게 말하기:" \
    && export LUAJIT_LIB=/usr/local/lib \
    && export LUAJIT_INC=/usr/local/include/luajit-2.0 \
    && echo "==================================================" \
    && echo "Downloading ngx_devel_kit" \
    && echo "==================================================" \
    && wget https://github.com/simplresty/ngx_devel_kit/archive/v0.3.1rc1.tar.gz -O /tmp/ngx_devel_kit.tar.gz \
    && cd /tmp && tar -xvzf ngx_devel_kit.tar.gz && mv ngx_devel_kit-* ngx_devel_kit \
    && echo "==================================================" \
    && echo "Downloading lua-nginx-module" \
    && echo "==================================================" \
    && wget https://github.com/openresty/lua-nginx-module/archive/v0.10.12rc2.tar.gz -O /tmp/lua-nginx-module.tar.gz \
    && cd /tmp && tar -xvzf lua-nginx-module.tar.gz && mv lua-nginx-module-* lua-nginx-module \
    && echo "==================================================" \
    && echo "Now Let's Installing NGINX" \
    && echo "==================================================" \
    && addgroup -S nginx \
    && adduser -D -S -h /var/cache/nginx -s /sbin/nologin -G nginx nginx \
    && wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz -O /tmp/nginx.tar.gz \
    && cd /tmp && tar -xvzf nginx.tar.gz \
    && cd nginx-${NGINX_VERSION} \
    && ./configure \
        --prefix=/etc/nginx \
        --sbin-path=/usr/sbin/nginx \
        --modules-path=/usr/lib/nginx/modules \
        --conf-path=/etc/nginx/nginx.conf \
        --pid-path=/var/run/nginx.pid \
        --lock-path=/var/run/nginx.lock \
        --http-log-path=/var/log/nginx/access.log \
        --error-log-path=/var/log/nginx/error.log \
        --user=nginx \
        --group=nginx \
        --with-pcre-jit \
        --with-http_ssl_module \
        --with-http_realip_module \
        --with-stream_ssl_module \
        --with-stream_realip_module \
        --with-http_stub_status_module \
        --with-http_gzip_static_module \
        --with-http_v2_module \
        --with-http_auth_request_module \
        --with-http_geoip_module \
        # in static module with <--add-module>
        --add-module=/tmp/nginx_accept_language_module \
        --add-module=/tmp/echo-nginx-module \
        # in dynamic modules compatibility with <--with-compat> <--add-dynamic-module>
        #--with-compat \
        #--add-dynamic-module=/tmp/nginx_accept_language_module-master \
        # ngx_cache_purge module
        --add-module=/tmp/ngx_cache_purge \
        # Lua-Nginx-Module
        --with-ld-opt="-Wl,-rpath,/usr/local/lib" \
        --add-module=/tmp/ngx_devel_kit \
        --add-module=/tmp/lua-nginx-module \
    && make -j$(getconf _NPROCESSORS_ONLN) \
    && make install \
    && echo "==================================================" \
    && echo "관련 디렉토리 링크및 생성하기" \
    && echo "==================================================" \
    && mkdir -p /etc/nginx/conf.d /var/www/html \
    && mv /etc/nginx/html/* /var/www/html/ && rm -rf /etc/nginx/html \
    && ln -s /usr/lib/nginx/modules /etc/nginx/modules \
    && echo "==================================================" \
    && echo "필요없는 파일 정리하기" \
    && echo "==================================================" \
    && apk del .build-deps \
    #&& rm /usr/lib/libGeoIP.a \
    && rm -rf /tmp/* \
    && rm -rf /var/cache/apk/*


# self-signed ssl for test
#RUN echo "skip line" \
#    && echo "==================================================" \
#    && echo "self-signed SSL certificate" \
#    && echo "==================================================" \
#    && mkdir /etc/nginx/ssl && cd /etc/nginx/ssl \
#    && openssl req \
#	    -subj '/CN=mydomain.com/O=John Doe/C=US' \
#	    -new -newkey rsa:2048 -sha256 -days 365 -nodes -x509 \
#	    -keyout server.key \
#	    -out server.crt

# ssl snippets & custom error pages
ADD provision/custom-errors /etc/nginx/

# 컨테이너안의 nginx 로그를 표준출력으로 보기 : https://docs.docker.com/engine/admin/logging/view_container_logs/
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

# 로컬파일 전송시에, Git for windows의 윈도우CRLF붙는 문제해결방안!
RUN echo "http://dl-4.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
    && apk --update add --no-cache dos2unix \
    && find /etc/nginx -type f -print0 | xargs -0 dos2unix \
    && apk del dos2unix

WORKDIR /var/www
EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]
