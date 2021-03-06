FROM alpine:3.6

# Taken from connexiolabs/alpine-nginx which appears dead (thanks!).
ENV NGINX_VERSION nginx-1.12.2

RUN \
	apk --update add \
	openssl-dev \
	pcre-dev \
	zlib-dev \
	wget \
	build-base \
	&& mkdir -p /tmp/src \
	&& cd /tmp/src \
	&& wget http://nginx.org/download/${NGINX_VERSION}.tar.gz \
	&& tar -zxvf ${NGINX_VERSION}.tar.gz \
	&& cd /tmp/src/${NGINX_VERSION} \
	&& ./configure \
	--with-http_ssl_module \
	--with-http_gzip_static_module \
	--prefix=/etc/nginx \
	--http-log-path=/var/log/nginx/access.log \
	--error-log-path=/var/log/nginx/error.log \
	--sbin-path=/usr/local/sbin/nginx \
	&& make \
	&& make install \
	&& apk del build-base \
	&& rm -rf /tmp/src \
	&& rm -rf /var/cache/apk/* \
	# forward request and error logs to docker log collector
	&& ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME /var/log/nginx

WORKDIR /etc/nginx

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
