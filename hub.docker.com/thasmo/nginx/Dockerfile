FROM debian:9
MAINTAINER Thomas "Thasmo" Deinhamer <hi@thasmo.com>

# Set build arguments.
ARG NGINX_USER="nginx"
ARG NGINX_VERSION=1.13.3
ARG NGINX_URL="https://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz"
ARG NCHAN_VERSION=1.1.7
ARG NCHAN_URL="https://github.com/slact/nchan/archive/v${NCHAN_VERSION}.tar.gz"
ARG ZLIB_VERSION=1.2.11
ARG ZLIB_URL="https://zlib.net/zlib-${ZLIB_VERSION}.tar.gz"

# Add our user/group first to ensure their IDs get set consistently.
RUN groupadd -r $NGINX_USER \
	&& useradd -r -g $NGINX_USER $NGINX_USER

# Install everything.
RUN set -x \

	# Install dependencies.
	&& apt-get update \
	&& apt-get install -y --no-install-recommends \
		build-essential \
		libpcre3-dev \
		libssl-dev \
		wget \
		ca-certificates \

	# Download Nginx.
	&& wget -qO- $NGINX_URL | tar -xzvC /tmp/ \

	# Download Nchan.
	&& wget -qO- $NCHAN_URL | tar -xzvC /tmp/ \

	# Download zlib.
	&& wget -qO- $ZLIB_URL | tar -xzvC /tmp/ \

	# Compile Nginx.
	&& cd /tmp/nginx-${NGINX_VERSION}/ \
	&& ./configure \
		--user=$NGINX_USER \
		--group=$NGINX_USER \
		--prefix=/etc/nginx \
		--sbin-path=/usr/sbin/nginx \
		--conf-path=/etc/nginx/nginx.conf \
		--pid-path=/var/run/nginx.pid \
		--lock-path=/var/run/nginx.lock \
		--error-log-path=/dev/stderr \
		--http-log-path=/dev/stdout \
		--with-pcre \
		--with-pcre-jit \
		--with-stream \
		--with-http_v2_module \
		--with-http_ssl_module \
		--with-zlib=/tmp/zlib-${ZLIB_VERSION}/ \
		--add-dynamic-module=/tmp/nchan-${NCHAN_VERSION}/ \
	&& make \
	&& make install \

	# Clean up.
	&& apt-get purge -y --auto-remove \
		build-essential \
		libpcre3-dev \
		libssl-dev \
		wget \
	&& apt-get clean \
	&& rm -rf \
		/var/lib/apt/lists/* \
		/var/tmp/* \
		/tmp/*

# Define exposed ports.
EXPOSE 80 443

# Set default command.
CMD ["nginx", "-g", "daemon off;"]
