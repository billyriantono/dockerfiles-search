#
# Streams 0.1
# Appbase, Inc
#

#
# Streams Dockerfile
#

FROM alpine:latest

MAINTAINER Guilherme Salazar <salazar@appbase.io>

ENV NGX_PATH="/tmp/ngx"
ENV STREAMS_PATH="${NGX_PATH}/streams"

ARG RESTY_VERSION="1.11.2.2"
ARG RESTY_OPENSSL_VERSION="1.0.2k"
ARG RESTY_PCRE_VERSION="8.40"
ARG NCHAN_VERSION="1.1.6"
ARG ROCKS_VERSION="2.4.2"
ARG RESTY_J="8"
ARG LUA_DEPS="lua-resty-http"

# 1) Install system dependencies
# 2) Get OpenResty, nchan, and LuaRocks
# 3) Build and install 2)
# 4) Install Lua dependencies
# 5) Clean our junk

RUN \
	mkdir /tmp/resty_build_area \
	&& cd /tmp/resty_build_area \
	# 1) Install system dependencies
	#
    && apk add --no-cache --virtual .build-deps \
		build-base \
		curl \
		perl-dev \
		zlib-dev \
		linux-headers \
	&& apk add --no-cache \
		libgcc \
		zlib \
		sed \
		apache2-utils \
	#
	# 2) Get OpenResty, nchan, and LuaRocks
	#
	&& curl -fSL https://openresty.org/download/openresty-${RESTY_VERSION}.tar.gz \
		-o openresty.tar.gz \
	&& curl -fSL https://github.com/slact/nchan/archive/v${NCHAN_VERSION}.tar.gz \
		-o nchan.tar.gz \
	&& curl -fSL https://luarocks.org/releases/luarocks-${ROCKS_VERSION}.tar.gz \
		-o luarocks.tar.gz \
	&& curl -fSL https://www.openssl.org/source/openssl-${RESTY_OPENSSL_VERSION}.tar.gz \
		-o openssl-${RESTY_OPENSSL_VERSION}.tar.gz \
	&& curl -fSL https://ftp.pcre.org/pub/pcre/pcre-${RESTY_PCRE_VERSION}.tar.gz \
		-o pcre-${RESTY_PCRE_VERSION}.tar.gz \
	&& curl -fSL https://raw.githubusercontent.com/siddharthlatest/mustache.sh/master/lib/mustache.sh \
		-o /usr/local/lib/mustache.sh \
	&& curl -fSL https://raw.githubusercontent.com/siddharthlatest/mustache.sh/master/bin/mustache.sh \
		-o /usr/local/bin/mustache.sh && chmod +x /usr/local/bin/mustache.sh \
	&& tar -xf openresty.tar.gz && tar -xf nchan.tar.gz && tar -xf luarocks.tar.gz \
	&& tar -xf openssl-${RESTY_OPENSSL_VERSION}.tar.gz \
	&& tar -xf pcre-${RESTY_PCRE_VERSION}.tar.gz \
	#
	# 3.1) Build and install OpenResty bundled with nchan
	#
	&& cd openresty-${RESTY_VERSION} \
	&& ./configure -j${RESTY_J} --add-module=../nchan-${NCHAN_VERSION} \
		--with-openssl=/tmp/resty_build_area/openssl-${RESTY_OPENSSL_VERSION} \
		--with-pcre=/tmp/resty_build_area/pcre-${RESTY_PCRE_VERSION} \
	&& make -j${RESTY_J} && make -j${RESTY_J} install \
	&& cd ../ \
	#
	# 3.2) Build and install LuaRocks to grab Lua dependencies
	#
	&& cd luarocks-${ROCKS_VERSION} \
	&& ./configure \
		--prefix=/usr/local/openresty/luajit \
		--with-lua=/usr/local/openresty/luajit \
		--lua-suffix=jit-2.1.0-beta2 \
		--with-lua-include=/usr/local/openresty/luajit/include/luajit-2.1 \
	&& make build && make install \
	&& cd ../ \
	#
	# 4) Install Lua dependencies
	#
	&& for dep in ${LUA_DEPS}; do \
			/usr/local/openresty/luajit/bin/luarocks install $dep; \
	done \
	#
	# 5) Clean up the work area
	#
	&& rm -rf /tmp/resty_build_area \
	&& apk del .build-deps \
	#
	# 6) Create nginx directories
	#
	&& mkdir -p ${NGX_PATH}/logs \
	&& touch ${NGX_PATH}/logs/{error,acces}.log \
	&& mkdir /ssl

COPY lua "${STREAMS_PATH}/lua"
COPY conf "${STREAMS_PATH}/conf"
COPY docker-entrypoint.sh "${STREAMS_PATH}/"

WORKDIR "${STREAMS_PATH}"

ENTRYPOINT ["/bin/sh", "docker-entrypoint.sh"]
