ARG ALPINE_VERSION=edge

########################
# Build pagespeed psol #
########################
FROM alpine:$ALPINE_VERSION as pagespeed

# Check https://github.com/apache/incubator-pagespeed-mod/tags
ARG MOD_PAGESPEED_TAG=v1.13.35.2

RUN apk add --no-cache \
        apache2-dev \
        apr-dev \
        apr-util-dev \
        build-base \
        curl \
        gettext-dev \
        git \
        gperf \
        icu-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        libressl-dev \
        pcre-dev \
        py-setuptools \
        zlib-dev \
    ;

WORKDIR /usr/src
RUN git clone -b ${MOD_PAGESPEED_TAG} \
              --recurse-submodules \
              --depth=1 \
              -c advice.detachedHead=false \
              -j`nproc` \
              https://github.com/apache/incubator-pagespeed-mod.git \
              modpagespeed \
    ;

WORKDIR /usr/src/modpagespeed

COPY patches/modpagespeed/*.patch ./

RUN for i in *.patch; do printf "\r\nApplying patch ${i%%.*}\r\n"; patch -p1 < $i || exit 1; done

WORKDIR /usr/src/modpagespeed/tools/gyp
RUN ./setup.py install

WORKDIR /usr/src/modpagespeed

RUN build/gyp_chromium --depth=. \
                       -D use_system_libs=1 \
    && \
    cd /usr/src/modpagespeed/pagespeed/automatic && \
    make psol BUILDTYPE=Release \
              CFLAGS+="-I/usr/include/apr-1" \
              CXXFLAGS+="-I/usr/include/apr-1 -DUCHAR_TYPE=uint16_t" \
              -j`nproc` \
    ;

RUN mkdir -p /usr/src/ngxpagespeed/psol/lib/Release/linux/x64 && \
    mkdir -p /usr/src/ngxpagespeed/psol/include/out/Release && \
    cp -R out/Release/obj /usr/src/ngxpagespeed/psol/include/out/Release/ && \
    cp -R pagespeed/automatic/pagespeed_automatic.a /usr/src/ngxpagespeed/psol/lib/Release/linux/x64/ && \
    cp -R net \
          pagespeed \
          testing \
          third_party \
          url \
          /usr/src/ngxpagespeed/psol/include/ \
    ;


##########################################
# Build Nginx with support for PageSpeed #
##########################################
FROM alpine:$ALPINE_VERSION AS nginx-builder

# Check https://github.com/apache/incubator-pagespeed-ngx/tags
ARG NGX_PAGESPEED_TAG=v1.13.35.2-stable

RUN apk add --no-cache \
        apr-dev \
        apr-util-dev \
        build-base \
        ca-certificates \
        gd-dev \
        geoip-dev \
        git \
        gnupg \
        icu-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        libxslt-dev \
        linux-headers \
        libressl-dev \
        pcre-dev \
        tar \
        zlib-dev \
    ;

WORKDIR /usr/src
RUN git clone -b ${NGX_PAGESPEED_TAG} \
              --recurse-submodules \
              --shallow-submodules \
              --depth=1 \
              -c advice.detachedHead=false \
              -j`nproc` \
              https://github.com/apache/incubator-pagespeed-ngx.git \
              ngxpagespeed \
    ;
############################ngx modules###################################
##depends from APKBUILD
##makedepends checkdepends
RUN apk add -U perl-dev libxml2-dev \
           gd perl perl-fcgi perl-io-socket-ssl perl-net-ssleay perl-protocol-websocket tzdata uwsgi-python \
           nginx nginx-mod-devel-kit
#ngx_http_substitutions_filter_module
RUN git clone \
              --depth=1 \
              -c advice.detachedHead=false \
              -j`nproc` \
              https://github.com/hongshunyang/ngx_http_substitutions_filter_module \
              ngx_http_substitutions_filter_module \
    ;
#ngx_http_geoip2_module
RUN apk add --no-cache libmaxminddb-dev \
&& git clone \
              --depth=1 \
              -c advice.detachedHead=false \
              -j`nproc` \
              https://github.com/leev/ngx_http_geoip2_module \
              ngx_http_geoip2_module \
    ;
#ngx_devel_kit required by ngx_set_misc 
RUN git clone \
              --depth=1 \
              -c advice.detachedHead=false \
              -j`nproc` \
	      https://github.com/simplresty/ngx_devel_kit.git \
              ngx_devel_kit \
    ;
#ngx_set_misc
RUN git clone \
              --depth=1 \
              -c advice.detachedHead=false \
              -j`nproc` \
	      https://github.com/openresty/set-misc-nginx-module.git \
              ngx_http_set_misc_module \
    ;
#ngx_memc
RUN git clone \
              --depth=1 \
              -c advice.detachedHead=false \
              -j`nproc` \
	      https://github.com/openresty/memc-nginx-module.git \
              ngx_http_memc_module \
    ;
#ngx_srcache
RUN git clone \
              --depth=1 \
              -c advice.detachedHead=false \
              -j`nproc` \
	      https://github.com/openresty/srcache-nginx-module.git \
              ngx_http_srcache_filter_module \
    ;
############################end############################################
RUN NGINX_VERSION=$(nginx -v 2>&1 |grep 'version'|awk -F "/" '{print $2}') \
&& wget https://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz

COPY --from=pagespeed /usr/src/ngxpagespeed /usr/src/ngxpagespeed/

WORKDIR /usr/src/nginx

RUN NGINX_VERSION=$(nginx -v 2>&1 |grep 'version'|awk -F "/" '{print $2}') \
&& NGINX_BUILD_CONFIG=$(nginx -V 2>&1 |grep 'configure' | awk -F ":" '{print $2}' | sed 's/^ *//g' | sed 's/ --add-dynamic-module=.*//g') \
&& tar zxf ../nginx-${NGINX_VERSION}.tar.gz --strip-components=1 -C . && \
    ./configure \
        ${NGINX_BUILD_CONFIG} \
        --add-dynamic-module=/usr/src/ngxpagespeed \
        --add-dynamic-module=/usr/src/ngx_http_substitutions_filter_module \
        --add-dynamic-module=/usr/src/ngx_http_geoip2_module \
        --add-dynamic-module=/usr/src/ngx_http_srcache_filter_module \
        --add-dynamic-module=/usr/src/ngx_http_memc_module \
        --add-dynamic-module=/usr/src/ngx_devel_kit \
        --add-dynamic-module=/usr/src/ngx_http_set_misc_module \
        --with-ld-opt="-Wl,-z,relro,--start-group -lapr-1 -laprutil-1 -licudata -licuuc -lpng -lturbojpeg -ljpeg" \
    && make \
    && make install -j`nproc`

RUN ln -s ../../usr/lib/nginx/modules /etc/nginx/modules && \
    strip /usr/lib/nginx/modules/*.so \
    ;


##########################################
# Combine everything with minimal layers #
##########################################
FROM nerelohw/docker-alpine:$ALPINE_VERSION

RUN apk add -U libjpeg-turbo libpng tiff giflib libwebp libwebp-tools tzdata \
libuuid apr apr-util icu icu-libs libressl pcre zlib libmaxminddb \
nginx \
nginx-mod-http-lua  \
nginx-mod-http-upload-progress  \
nginx-mod-devel-kit  \
nginx-mod-http-echo  \
nginx-mod-http-fancyindex  \
nginx-mod-http-geoip  \
nginx-mod-http-headers-more  \
&& rm -rf /var/cache/apk/*

COPY --from=pagespeed /usr/bin/envsubst /usr/local/bin
COPY --from=nginx-builder /usr/lib/nginx/modules/ngx_pagespeed.so /usr/lib/nginx/modules/
COPY --from=nginx-builder /usr/lib/nginx/modules/ngx_http_geoip2_module.so /usr/lib/nginx/modules/
COPY --from=nginx-builder /usr/lib/nginx/modules/ngx_stream_geoip2_module.so /usr/lib/nginx/modules/
COPY --from=nginx-builder /usr/lib/nginx/modules/ngx_http_subs_filter_module.so /usr/lib/nginx/modules/
COPY --from=nginx-builder /usr/lib/nginx/modules/ngx_http_srcache_filter_module.so /usr/lib/nginx/modules/
COPY --from=nginx-builder /usr/lib/nginx/modules/ngx_http_memc_module.so /usr/lib/nginx/modules/
COPY --from=nginx-builder /usr/lib/nginx/modules/ngx_http_set_misc_module.so /usr/lib/nginx/modules/

RUN echo 'load_module "modules/ngx_pagespeed.so";'> /etc/nginx/modules/ngx_pagespeed.conf \
&& echo 'load_module "modules/ngx_http_geoip2_module.so";'> /etc/nginx/modules/http_geoip2.conf \
&& echo 'load_module "modules/ngx_http_subs_filter_module.so";'> /etc/nginx/modules/http_subs_filter.conf \
&& echo 'load_module "modules/ngx_http_srcache_filter_module.so";'> /etc/nginx/modules/http_srcache_filter.conf \
&& echo 'load_module "modules/ngx_http_memc_module.so";'> /etc/nginx/modules/http_memc.conf \
&& echo 'load_module "modules/ngx_http_set_misc_module.so";'> /etc/nginx/modules/http_memc.conf \
&& install -g nginx -o nginx -d /var/cache/ngx_pagespeed

RUN mkdir -p /run/nginx

EXPOSE 80 443

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
