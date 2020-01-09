FROM debian:stable-slim

RUN cd \
    && apt update && apt full-upgrade -y \
    && apt install -y \
        ca-certificates \
        wget \
        curl \
        git \
        bzip2 \
        build-essential \
        xsltproc \
        uuid-dev \
        zlib1g-dev \
        libxslt1-dev \
        libpcre3-dev \
        libgd-dev \
        libgeoip-dev \
        libperl-dev \
        gettext-base \
        | tee build-deps.txt \
    && update-ca-certificates \
    && JEMALLOC_VERSION=$(curl -sS --fail https://github.com/jemalloc/jemalloc/releases | \
        grep -o '/jemalloc-[a-zA-Z0-9.]*[.]tar[.]bz2' | \
        sed -e 's~^/jemalloc-~~' -e 's~\.tar\.bz2$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget https://github.com/jemalloc/jemalloc/releases/download/${JEMALLOC_VERSION}/jemalloc-${JEMALLOC_VERSION}.tar.bz2 \
    && tar -xjvf jemalloc-${JEMALLOC_VERSION}.tar.bz2 \
    && JEMALLOC_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*jemalloc-${JEMALLOC_VERSION}*") \
    && REDIS_VERSION=$(curl -sS --fail https://github.com/antirez/redis/releases | \
        grep -o '/antirez/redis/archive/[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/antirez/redis/archive/~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget -O redis-${REDIS_VERSION}.tar.gz https://github.com/antirez/redis/archive/${REDIS_VERSION}.tar.gz \
    && tar -xvzf redis-${REDIS_VERSION}.tar.gz \
    && REDIS_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*redis-${REDIS_VERSION}*") \
    && OPENSSL_VERSION=$(curl -sS --fail https://www.openssl.org/source/ | \
        grep -o 'openssl-[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^openssl-~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget https://www.openssl.org/source/openssl-${OPENSSL_VERSION}.tar.gz \
    && tar -xvzf openssl-${OPENSSL_VERSION}.tar.gz \
    && OPENSSL_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*openssl-${OPENSSL_VERSION}*") \
    && NGINX_VERSION=$(curl -sS --fail https://nginx.org/en/download.html | \
        grep -o '/download/nginx-[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/download/nginx-~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
    && tar -xvzf nginx-${NGINX_VERSION}.tar.gz \
    && NGINX_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*nginx-${NGINX_VERSION}*") \
    && NJS_VERSION=$(curl -sS --fail https://github.com/nginx/njs/releases | \
        grep -o '/nginx/njs/archive/[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/nginx/njs/archive/~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget -O njs-${NJS_VERSION}.tar.gz https://github.com/nginx/njs/archive/${NJS_VERSION}.tar.gz \
    && tar -xvzf njs-${NJS_VERSION}.tar.gz \
    && NJS_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*njs-${NJS_VERSION}*") \
    && NCP_VERSION=$(curl -sS --fail https://github.com/FRiCKLE/ngx_cache_purge/releases | \
        grep -o '/ngx_cache_purge/archive/[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/ngx_cache_purge/archive/~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget -O ncp-${NCP_VERSION}.tar.gz https://github.com/FRiCKLE/ngx_cache_purge/archive/${NCP_VERSION}.tar.gz \
    && tar -xvzf ncp-${NCP_VERSION}.tar.gz \
    && NCP_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*ngx_cache_purge-${NCP_VERSION}*") \
    && git clone -j`nproc` https://github.com/google/ngx_brotli \
    && NB_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*ngx_brotli*") \
    && cd $NB_DIR \
    && git submodule update --init \
    && cd \
    && NPS_VERSION=$(curl -sS --fail https://github.com/apache/incubator-pagespeed-ngx/releases | \
        grep -o '/incubator-pagespeed-ngx/archive/v[a-zA-Z0-9.]*-stable[.]tar[.]gz' | \
        sed -e 's~^/incubator-pagespeed-ngx/archive/v~~' -e 's~\-stable\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget -O nps-v${NPS_VERSION}-stable.tar.gz https://github.com/apache/incubator-pagespeed-ngx/archive/v${NPS_VERSION}-stable.tar.gz \
    && tar -xvzf nps-v${NPS_VERSION}-stable.tar.gz \
    && NPS_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*incubator-pagespeed-ngx-${NPS_VERSION}-stable*") \
    && cd "$NPS_DIR" \
    && [ -e scripts/format_binary_url.sh ] && PSOL_URL=$(scripts/format_binary_url.sh PSOL_BINARY_URL) \
    && wget ${PSOL_URL} \
    && tar -xvzf $(basename ${PSOL_URL}) \
    && cd \
    && NHR_VERSION=$(curl -sS --fail https://www.nginx.com/resources/wiki/modules/redis/ | \
        grep -o '/ngx_http_redis-[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/ngx_http_redis-~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget https://people.freebsd.org/~osa/ngx_http_redis-${NHR_VERSION}.tar.gz \
    && tar -xvzf ngx_http_redis-${NHR_VERSION}.tar.gz \
    && NHR_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*ngx_http_redis-${NHR_VERSION}*") \
    && NDK_VERSION=$(curl -sS --fail https://github.com/simplresty/ngx_devel_kit/releases | \
        grep -o '/ngx_devel_kit/archive/v[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/ngx_devel_kit/archive/v~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget -O ndk-v${NDK_VERSION}.tar.gz https://github.com/simplresty/ngx_devel_kit/archive/v${NDK_VERSION}.tar.gz \
    && tar -xvzf ndk-v${NDK_VERSION}.tar.gz \
    && NDK_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*ngx_devel_kit-${NDK_VERSION}*") \
    && SMNM_VERSION=$(curl -sS --fail https://github.com/openresty/set-misc-nginx-module/releases | \
        grep -o '/set-misc-nginx-module/archive/v[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/set-misc-nginx-module/archive/v~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget -O smnm-v${SMNM_VERSION}.tar.gz https://github.com/openresty/set-misc-nginx-module/archive/v${SMNM_VERSION}.tar.gz \
    && tar -xvzf smnm-v${SMNM_VERSION}.tar.gz \
    && SMNM_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*set-misc-nginx-module-${SMNM_VERSION}*") \
    && ENM_VERSION=$(curl -sS --fail https://github.com/openresty/echo-nginx-module/releases | \
        grep -o '/echo-nginx-module/archive/v[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/echo-nginx-module/archive/v~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget -O enm-v${ENM_VERSION}.tar.gz https://github.com/openresty/echo-nginx-module/archive/v${ENM_VERSION}.tar.gz \
    && tar -xvzf enm-v${ENM_VERSION}.tar.gz \
    && ENM_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*echo-nginx-module-${ENM_VERSION}*") \
    && R2NM_VERSION=$(curl -sS --fail https://github.com/openresty/redis2-nginx-module/releases | \
        grep -o '/redis2-nginx-module/archive/v[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/redis2-nginx-module/archive/v~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget -O r2nm-v${R2NM_VERSION}.tar.gz https://github.com/openresty/redis2-nginx-module/archive/v${R2NM_VERSION}.tar.gz \
    && tar -xvzf r2nm-v${R2NM_VERSION}.tar.gz \
    && R2NM_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*redis2-nginx-module-${R2NM_VERSION}*") \
    && SNM_VERSION=$(curl -sS --fail https://github.com/openresty/srcache-nginx-module/releases | \
        grep -o '/srcache-nginx-module/archive/v[a-zA-Z0-9.]*[.]tar[.]gz' | \
        sed -e 's~^/srcache-nginx-module/archive/v~~' -e 's~\.tar\.gz$~~' | \
        sed '/alpha.*/Id' | \
        sed '/pre.*/Id' | \
        sed '/beta.*/Id' | \
        sed '/rc.*/Id' | \
        sort -t '.' -k 1,1 -k 2,2 -k 3,3 -k 4,4 -g | \
        tail -n 1) \
    && wget -O snm-v${SNM_VERSION}.tar.gz https://github.com/openresty/srcache-nginx-module/archive/v${SNM_VERSION}.tar.gz \
    && tar -xvzf snm-v${SNM_VERSION}.tar.gz \
    && SNM_DIR=$(find $HOME -maxdepth 1 -mindepth 1 -type d -name "*srcache-nginx-module-${SNM_VERSION}*") \
    && cd $JEMALLOC_DIR \
    && ./configure --prefix=/usr \
    && make -j`nproc` \
    && make install_lib_shared -j`nproc` \
    && strip /usr/lib/libjemalloc* \
    && sed -ri 's!^(#define CONFIG_DEFAULT_PROTECTED_MODE) 1$!\1 0!' $REDIS_DIR/src/server.h \
    && cd $REDIS_DIR \
    && make -j`nproc` \
    && make PREFIX=/usr install -j`nproc` \
    && strip /usr/bin/redis* \
    && cd $NGINX_DIR \
    && ./configure \
        --prefix=/etc/nginx \
        --sbin-path=/usr/sbin/nginx \
        --modules-path=/usr/lib/nginx/modules \
        --conf-path=/etc/nginx/nginx.conf \
        --error-log-path=/var/log/nginx/error.log \
        --http-log-path=/var/log/nginx/access.log \
        --pid-path=/var/run/nginx/nginx.pid \
        --lock-path=/var/run/nginx/nginx.lock \
        --http-client-body-temp-path=/var/cache/nginx/client_temp \
        --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
        --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
        --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
        --http-scgi-temp-path=/var/cache/nginx/scgi_temp \
        --user=nginx \
        --group=nginx \
        --with-http_ssl_module \
        --with-http_realip_module \
        --with-http_addition_module \
        --with-http_sub_module \
        --with-http_dav_module \
        --with-http_flv_module \
        --with-http_mp4_module \
        --with-http_gunzip_module \
        --with-http_gzip_static_module \
        --with-http_random_index_module \
        --with-http_secure_link_module \
        --with-http_stub_status_module \
        --with-http_auth_request_module \
        --with-http_xslt_module=dynamic \
        --with-http_image_filter_module=dynamic \
        --with-http_geoip_module=dynamic \
        --with-http_perl_module=dynamic \
        --with-threads \
        --with-stream=dynamic \
        --with-stream_ssl_module \
        --with-stream_ssl_preread_module \
        --with-stream_realip_module \
        --with-stream_geoip_module=dynamic \
        --with-http_slice_module \
        --with-mail=dynamic \
        --with-mail_ssl_module \
        --with-compat \
        --with-file-aio \
        --with-http_v2_module \
        --add-dynamic-module=$NJS_DIR//nginx \
        --with-ld-opt='-ljemalloc' \
        --with-openssl=$OPENSSL_DIR \
        --add-module=$NCP_DIR \
        --add-dynamic-module=$NB_DIR \
        --add-dynamic-module=$NPS_DIR \
        --add-dynamic-module=$NHR_DIR \
        --add-dynamic-module=$NDK_DIR \
        --add-dynamic-module=$SMNM_DIR \
        --add-dynamic-module=$ENM_DIR \
        --add-dynamic-module=$R2NM_DIR \
        --add-dynamic-module=$SNM_DIR \
    && make -j`nproc` \
    && make install -j`nproc` \
    && strip /usr/sbin/nginx* \
    && strip /usr/lib/nginx/modules/*.so \
    && cd \
    && rm -rf \
        /etc/nginx/nginx.conf \
        /etc/nginx/nginx.conf.default \
        /etc/nginx/uwsgi_params.default \
        /etc/nginx/scgi_params.default \
        /etc/nginx/mime.types.default \
        /etc/nginx/fastcgi_params.default \
        /etc/nginx/fastcgi.conf.default \
    && ldd /usr/lib/libjemalloc* \
        /usr/bin/redis* \
        /usr/bin/envsubst* \
        /usr/sbin/nginx* \
        /usr/lib/nginx/modules/*.so | \
        cut -d ">" -f 2 | \
        cut -d "(" -f 1 | \
        cut -d ":" -f 1 | \
        sed '/linux-vdso.*/d' | \
        sed '/not a dynamic executable.*/d' | \
        sed 's/^[ \t]*//g' | \
        sed 's/[ \t]*$//g' | \
        sort -u | \
        tee software-deps.txt \
    && readlink -f $(cat software-deps.txt) | \
        sort -u | \
        tee symlink-source.txt \
    && cat software-deps.txt \
        symlink-source.txt | \
        sort -u | \
        xargs tar -cvpPf software-package.tar \
    && mkdir -p \
        /etc/redis \
        /etc/redis_default \
        /var/log/redis \
        /var/lib/redis \
        /var/run/redis \
    && adduser  \
        --system  \
        --home /var/lib/redis \
        --shell /bin/false \
        --group \
        --disabled-login \
        --quiet \
        redis \
    && wget -O /etc/redis_default/redis.conf https://raw.githubusercontent.com/Xaster/docker-nginx-debian/master/config/etc/redis/redis.conf \
    && chown redis:redis /etc/redis_default/redis.conf \
    && chown redis:adm /var/log/redis \
    && chown redis:redis /var/run/redis \
    && mkdir -p \
        /usr/share/nginx/html \
        /usr/share/nginx/html_default \
        /etc/nginx_default/conf.d \
        /etc/certs \
        /var/log/nginx \
        /var/cache/nginx \
        /var/run/nginx \
    && adduser \
        --system \
        --home /var/cache/nginx \
        --shell /bin/false \
        --group \
        --disabled-login \
        --quiet \
        nginx \
    && mv -f /etc/nginx/html/index.html \
        /etc/nginx/html/50x.html \
        /usr/share/nginx/html_default \
    && rm -rf /etc/nginx/html \
    && chown -R nginx:nginx /usr/share/nginx/html \
    && mv -f /etc/nginx/* /etc/nginx_default \
    && wget -O /etc/nginx_default/nginx.conf https://raw.githubusercontent.com/Xaster/docker-nginx-debian/master/config/etc/nginx/nginx.conf \
    && wget -O /etc/nginx_default/conf.d/default.conf https://raw.githubusercontent.com/Xaster/docker-nginx-debian/master/config/etc/nginx/conf.d/default.conf \
    && wget -O /usr/bin/CMD-Shell https://raw.githubusercontent.com/Xaster/docker-nginx-debian/master/CMD-Shell \
    && chmod +x /usr/bin/CMD-Shell \
    && apt purge --auto-remove -y \
        $(cat build-deps.txt | \
        grep "Unpacking " | \
        cut -d " " -f 2) \
    && apt install -y tzdata \
    && tar --skip-old-files -xpPf software-package.tar \
    && apt clean \
    && rm -rf \
        $HOME/* \
        /var/lib/apt/lists/*\
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/usr/share/nginx/html", "/etc/nginx", "/etc/certs", "/var/log/nginx", "/var/cache/nginx", "/var/run/nginx", "/etc/redis", "/var/log/redis", "/var/lib/redis", "/var/run/redis"]
EXPOSE 80 443 6379
ENV TIMEZONE=""

CMD ["CMD-Shell"]
