FROM debian:jessie

ENV NGINX_VERSION 1.12.0
ENV NGINX_DK_VERSION 0.3.0
ENV NGINX_SM_VERSION 0.31
ENV NGINX_CP_VERSION 2.3
ENV NGINX_PS_VERSION 1.11.33.4

RUN set -ex \
  \
  && buildDeps=" \
      build-essential \
      libssl-dev \
      zlib1g-dev \
      libpcre3-dev \
      libgd-dev \
      libgeoip-dev \
     " \
  && fetchDeps=" \
      unzip \
      wget \
     " \
  && apt-get update \
  && apt-get install --no-install-recommends --no-install-suggests -y \
    ca-certificates \
    libssl1.0.0 \
    zlib1g \
    libpcre3 \
    libgd3 \
    libgeoip1 \
    ${buildDeps} \
    ${fetchDeps} \
  && rm -rf /var/lib/apt/lists/* \
  && mkdir -p /usr/src \
  && cd /usr/src \
  \
  && wget -O nginx.tar.gz "http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz" \
  && tar -xzf nginx.tar.gz -C /usr/src/ \
  \
  && wget -O ngx_devel_kit.tar.gz "https://github.com/simpl/ngx_devel_kit/archive/v${NGINX_DK_VERSION}.tar.gz" \
  && tar -xzf ngx_devel_kit.tar.gz -C /usr/src/ \
  \
  && wget -O set-misc-nginx.tar.gz "https://github.com/openresty/set-misc-nginx-module/archive/v${NGINX_SM_VERSION}.tar.gz" \
  && tar -xzf set-misc-nginx.tar.gz -C /usr/src/ \
  \
  && wget -O ngx_cache_purge.tar.gz "https://github.com/FRiCKLE/ngx_cache_purge/archive/${NGINX_CP_VERSION}.tar.gz" \
  && tar -xzf ngx_cache_purge.tar.gz -C /usr/src/ \
  \
  && wget -O ngx_pagespeed.zip "https://github.com/pagespeed/ngx_pagespeed/archive/v${NGINX_PS_VERSION}-beta.zip" \
  && unzip ngx_pagespeed.zip \
  \
  && wget -O psol.tar.gz "https://dl.google.com/dl/page-speed/psol/${NGINX_PS_VERSION}.tar.gz" \
  && tar -xzf psol.tar.gz -C /usr/src/ngx_pagespeed-${NGINX_PS_VERSION}-beta \
  \
  && cd /usr/src/nginx-${NGINX_VERSION} \
  && ./configure \
    --prefix=/etc/nginx \
    --sbin-path=/usr/sbin/nginx \
    --modules-path=/usr/lib/nginx/modules \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --pid-path=/var/run/nginx.pid \
    --lock-path=/var/run/nginx.lock \
    --http-client-body-temp-path=/var/cache/nginx/client_temp \
    --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
    --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
    --user=nginx --group=nginx \
    --with-pcre-jit \
    --with-threads \
    --with-file-aio \
    --without-http_scgi_module \
    --without-http_uwsgi_module \
    --with-http_addition_module \
    --with-http_auth_request_module \
    --with-http_gunzip_module \
    --with-http_gzip_static_module \
    --with-http_mp4_module \
    --with-http_image_filter_module=dynamic \
    --with-http_geoip_module=dynamic \
    --with-http_realip_module \
    --with-http_secure_link_module \
    --with-http_slice_module \
    --with-http_ssl_module \
    --with-http_sub_module \
    --with-http_v2_module \
    --with-http_stub_status_module \
    --with-cc-opt='-g -O2 -fstack-protector-strong -Wformat -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2' \
    --with-ld-opt='-Wl,-z,relro -Wl,-z,now -Wl,--as-needed' \
    --add-dynamic-module=/usr/src/ngx_devel_kit-${NGINX_DK_VERSION} \
    --add-dynamic-module=/usr/src/set-misc-nginx-module-${NGINX_SM_VERSION} \
    --add-module=/usr/src/ngx_cache_purge-${NGINX_CP_VERSION} \
    --add-dynamic-module=/usr/src/ngx_pagespeed-${NGINX_PS_VERSION}-beta \
    && make \
    && make install \
    \
    # create modules symlink
    && ln -s /usr/lib/nginx/modules /etc/nginx/modules \
    && apt-get purge -y --auto-remove \
      ${buildDeps} \
      ${fetchDeps} \
    && rm -rf /usr/src


# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
