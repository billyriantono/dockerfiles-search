# vim:set ft=dockerfile:

# Base off VRT's base nginx image
FROM vrtsystems/nginx:0.2.2
MAINTAINER VRT Engineering <engineering@vrt.com.au>

# Override with --build-arg var=value
ARG NGINX_MOD_URI=https://github.com/vrtsystems/nginx-dav-ext-module.git
ARG NGINX_MOD_BRANCH=develop
ARG NGINX_MOD_DIR=/usr/lib/nginx/modules

# The ./configure file came out of the rules file of the nginx Debian packages.
# nginx, unlike Apache, has a very monolithic build system and requires you to
# have a copy of the source build tree around.
RUN echo "=== Installing nginx-dav-ext-module =============" \
	&& cd /tmp \
	&& echo "deb-src http://nginx.org/packages/mainline/debian/ jessie nginx" \
		>> /etc/apt/sources.list.d/nginx-src.list \
	&& apt-get update \
	&& apt-get install -y libexpat1-dev dpkg-dev \
	&& apt-get build-dep -y nginx=${NGINX_VERSION} \
	&& apt-get source nginx=${NGINX_VERSION} \
	&& git clone --depth 1 --branch ${NGINX_MOD_BRANCH} \
		${NGINX_MOD_URI} nginx-mod \
	&& cd /tmp/nginx-[0-9]* \
	&& ./configure \
		--prefix=/etc/nginx --sbin-path=/usr/sbin/nginx \
		--modules-path=${NGINX_MOD_DIR} \
		--conf-path=/etc/nginx/nginx.conf \
		--error-log-path=/var/log/nginx/error.log \
		--http-log-path=/var/log/nginx/access.log \
		--pid-path=/var/run/nginx.pid \
		--lock-path=/var/run/nginx.lock \
		--http-client-body-temp-path=/var/cache/nginx/client_temp \
		--http-proxy-temp-path=/var/cache/nginx/proxy_temp \
		--http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
		--http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
		--http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx \
		--group=nginx --with-compat --with-file-aio --with-threads \
		--with-http_addition_module --with-http_auth_request_module \
		--with-http_dav_module --with-http_flv_module \
		--with-http_gunzip_module --with-http_gzip_static_module \
		--with-http_mp4_module --with-http_random_index_module \
		--with-http_realip_module --with-http_secure_link_module \
		--with-http_slice_module --with-http_ssl_module \
		--with-http_stub_status_module --with-http_sub_module \
		--with-http_v2_module --with-mail --with-mail_ssl_module \
		--with-stream --with-stream_realip_module \
		--with-stream_ssl_module --with-stream_ssl_preread_module \
		--add-dynamic-module=/tmp/nginx-mod \
		--with-cc-opt="" --with-ld-opt="" \
	&& make modules \
	&& install -t /usr/lib/nginx/modules objs/*.so \
	&& echo "=== Cleaning up ========================" \
	&& cd / \
	&& rm -fr /tmp/nginx-* \
	&& apt-get purge -y libexpat1-dev dpkg-dev \
	&& /usr/local/sbin/docker-cleanup.sh
