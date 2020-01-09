FROM nginx:1.15.8
MAINTAINER staslapshin88@gmail.com

ENV MAXMIND_VERSION=1.3.2
ENV NGINX_SHORT_VERSION=1.15.8

RUN set -x && DEBIAN_FRONTEND=noninteractive apt-get update \
  && apt-get install --no-install-recommends -y \
    build-essential \
    ca-certificates \
    dpkg-dev \
    git \
    libssl-dev \
    libpcre3-dev \
    zlib1g-dev \
    wget \
    libxslt-dev \
    libgeoip-dev \
    libgd-dev 

# Install Maxmind db library

RUN set -x \
  && wget https://github.com/maxmind/libmaxminddb/releases/download/${MAXMIND_VERSION}/libmaxminddb-${MAXMIND_VERSION}.tar.gz \
  && tar xf libmaxminddb-${MAXMIND_VERSION}.tar.gz \
  && cd libmaxminddb-${MAXMIND_VERSION} \
  && ./configure \
  && make \
  && make check \
  && make install \
  && ldconfig

# Install nginx extension for GeoIP2. See: https://github.com/leev/ngx_http_geoip2_module
# We have to recompile nginx. To keep things simple we use the deb file + the same compile options as before.
#
# NGINX_VERSION is coming from the base container
#
# FIXME: use nginx -V to use current compile options
#        NGINX_OPTIONS=$(2>&1 nginx -V | grep 'configure arguments' | awk -F: '{print $2}') \
RUN set -x \
  && git clone https://github.com/leev/ngx_http_geoip2_module \
  && echo "deb-src http://nginx.org/packages/mainline/debian/ stretch nginx" >> /etc/apt/sources.list \
  && DEBIAN_FRONTEND=noninteractive apt-get update \
  && tempDir="$(mktemp -d)" \
  && chmod 777 "$tempDir" \
  && cd "$tempDir" \
  && apt-get source nginx=${NGINX_VERSION} \
  && ls -la \
  && cd nginx-${NGINX_SHORT_VERSION} \
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
    --with-threads \
    --with-stream \
    --with-stream_ssl_module \
    --with-stream_ssl_preread_module \
    --with-stream_realip_module \
    --with-stream_geoip_module=dynamic \
    --with-http_slice_module \
    --with-mail \
    --with-mail_ssl_module \
    --with-compat \
    --with-file-aio \
    --with-http_v2_module \
    --add-dynamic-module=/ngx_http_geoip2_module \
  && make modules \
  && cp objs/ngx_http_geoip2_module.so /usr/lib/nginx/modules/ \
  && apt-get remove --purge -y \
    build-essential \
    dpkg-dev

# Download Maxmind db version 2
# This example uses the free version from https://dev.maxmind.com/geoip/geoip2/geolite2/
#
# We only use the country db, you can add the city db and others if you want them.
RUN set -x && mkdir -p /usr/share/geoip \
  && wget -O /tmp/country.tar.gz http://geolite.maxmind.com/download/geoip/database/GeoLite2-Country.tar.gz \
  && tar xf /tmp/country.tar.gz -C /usr/share/geoip --strip 1 \
  && ls -al /usr/share/geoip/
