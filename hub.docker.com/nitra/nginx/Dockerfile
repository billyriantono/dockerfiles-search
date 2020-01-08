FROM pagespeed/nginx-pagespeed:1.13.35-alpine3.8-ngx1.15 AS subs

ARG NGINX_VERSION=1.15.4
ARG NGINX_PGPKEY=520A9993A1C052F8

RUN apk add --update --no-cache --virtual .build-deps \
	    gcc \
	    libc-dev \
	    make \
	    openssl-dev \
	    pcre-dev \
	    zlib-dev \
	    linux-headers \
	    gnupg \
	    libxslt-dev \
	    gd-dev \
	    geoip-dev \
	    autoconf \
	    automake \
	    libtool \
	    git
RUN wget "https://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz" \
         "https://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz.asc" && \
    (gpg --keyserver ha.pool.sks-keyservers.net --keyserver-options timeout=10 --recv-keys "${NGINX_PGPKEY}" || \
     gpg --keyserver hkp://keyserver.ubuntu.com:80 --keyserver-options timeout=10 --recv-keys "${NGINX_PGPKEY}" || \
     gpg --keyserver hkp://p80.pool.sks-keyservers.net:80 --keyserver-options timeout=10 --recv-keys "$NGINX_PGPKEY}" ) && \
    gpg --trusted-key "${NGINX_PGPKEY}" --verify "nginx-${NGINX_VERSION}.tar.gz.asc"
RUN wget -O subs.tar.gz https://api.github.com/repos/nginxinc/ngx_http_substitutions_filter_module/tarball/nginx
RUN mkdir -p /usr/src 
RUN tar -zxC /usr/src -f subs.tar.gz 
RUN tar -zxC /usr/src -f "nginx-${NGINX_VERSION}.tar.gz"
WORKDIR /usr/src/nginx-"${NGINX_VERSION}"
RUN ./configure --with-compat --add-dynamic-module=/usr/src/nginxinc-ngx_http_substitutions_filter_module-3e96a0c 
RUN make --jobs="$(getconf _NPROCESSORS_ONLN)"

FROM pagespeed/nginx-pagespeed:1.13.35-alpine3.8-ngx1.15

ENV VER ps1 

ARG NGINX_VERSION=1.15.4

COPY --from=subs "/usr/src/nginx-${NGINX_VERSION}/objs/ngx_http_subs_filter_module.so" "/etc/nginx/modules/ngx_http_subs_filter_module.so"
COPY auto-reload-nginx.sh .
COPY check.sh .

RUN sed -i -e "1 s/^/load_module \\/etc\\/nginx\\/modules\\/ngx_http_subs_filter_module.so\\; \\n/;" /etc/nginx/nginx.conf \
&& apk --no-cache add --update \
inotify-tools \
curl \
&& rm /etc/nginx/conf.d/default.conf 

CMD ["/auto-reload-nginx.sh"]