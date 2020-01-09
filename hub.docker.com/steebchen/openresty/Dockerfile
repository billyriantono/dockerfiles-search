FROM ubuntu:xenial

RUN apt-get -y update \
	&& apt-get -y upgrade \
	&& apt-get install -y software-properties-common \
	&& add-apt-repository ppa:maxmind/ppa \
	&& apt-get -y update \
	&& apt-get install -y \
	libpcre3 \
	libpcre3-dev \
	libssl-dev \
	libperl4-corelibs-perl \
	libmaxminddb0 libmaxminddb-dev mmdb-bin \
	g++ \
	cmake \
	unzip \
	wget \
	curl \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/krallin/tini/releases/download/v0.18.0/tini -O /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

# MongoDB C driver
RUN wget https://github.com/mongodb/mongo-c-driver/releases/download/1.13.0/mongo-c-driver-1.13.0.tar.gz \
	&& tar -xvzf mongo-c-driver-1.13.0.tar.gz \
	&& rm mongo-c-driver-1.13.0.tar.gz \
	&& cd mongo-c-driver-1.13.0 \
	&& mkdir cmake-build \
	&& cd cmake-build \
	&& cmake -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF .. \
	&& make \
	&& make install \
	&& cd ../.. \
	&& rm -r mongo-c-driver-1.13.0

# GeoLite2
RUN mkdir /modules \
	&& cd /modules \
	&& wget https://github.com/leev/ngx_http_geoip2_module/archive/3.2.tar.gz \
	&& tar -xvzf 3.2.tar.gz \
	&& rm 3.2.tar.gz

# Openresty
RUN wget https://github.com/openresty/openresty/releases/download/v1.13.6.1/openresty-1.13.6.1.tar.gz \
	&& tar -xvf openresty-1.13.6.1.tar.gz \
	&& rm openresty-1.13.6.1.tar.gz \
	&& cd openresty-1.13.6.1/ \
	&& ./configure -j2 \
		--add-module=/modules/ngx_http_geoip2_module-3.2 \
		--with-http_v2_module \
		--with-ipv6 \
	&& make -j2 \
	&& make install \
	&& cd .. \
	&& rm -r openresty-1.13.6.1

# Lua BSON module
ENV LUA_CBSON_SHA=6af9aee63895e3a538a879a155ecdea0b7325941
RUN wget https://github.com/isage/lua-cbson/archive/$LUA_CBSON_SHA.zip \
	&& unzip $LUA_CBSON_SHA.zip \
	&& rm $LUA_CBSON_SHA.zip \
	&& cd lua-cbson-$LUA_CBSON_SHA \
	&& mkdir build \
	&& cd build \
	&& cmake .. \
	&& make \
	&& make install \
	&& ldconfig \
	&& cd ../.. \
	&& rm -r lua-cbson-$LUA_CBSON_SHA

# Lua MongoDB client module
ENV LUA_MOONGOO_SHA=ca544d1ba0dda0c705bfe1123733bff2cd43633a
RUN wget https://github.com/isage/lua-resty-moongoo/archive/$LUA_MOONGOO_SHA.zip \
	&& unzip $LUA_MOONGOO_SHA.zip \
	&& rm $LUA_MOONGOO_SHA.zip \
	&& cp -r lua-resty-moongoo-$LUA_MOONGOO_SHA/lib/resty/* /usr/local/openresty/lualib/resty \
	&& ls -lah /usr/local/openresty/lualib/resty \
	&& rm -r lua-resty-moongoo-$LUA_MOONGOO_SHA

RUN wget http://luarocks.org/releases/luarocks-2.0.13.tar.gz \
	&& tar -xzvf luarocks-2.0.13.tar.gz \
	&& rm luarocks-2.0.13.tar.gz \
	&& cd luarocks-2.0.13/ \
	&& ./configure --prefix=/usr/local/openresty/luajit \
		--with-lua=/usr/local/openresty/luajit/ \
		--lua-suffix=jit \
		--with-lua-include=/usr/local/openresty/luajit/include/luajit-2.1 \
	&& make \
	&& make install

ENV PATH="/usr/local/openresty/bin:/usr/local/openresty/nginx/sbin:/usr/local/openresty/luajit/bin:${PATH}"

RUN opm get thibaultcha/lua-resty-mlcache
RUN luarocks install lua-resty-auto-ssl

ADD http://geolite.maxmind.com/download/geoip/database/GeoLite2-ASN.tar.gz /var/lib/nginx/
ADD http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.tar.gz /var/lib/nginx/

RUN cd /var/lib/nginx/ \
	&& tar --strip-components=1 -xzf GeoLite2-ASN.tar.gz \
	&& rm GeoLite2-ASN.tar.gz \
	&& tar --strip-components=1 -xzf GeoLite2-City.tar.gz \
	&& rm GeoLite2-City.tar.gz

# connect stdout & stderr
RUN ln -sf /dev/stdout /usr/local/openresty/nginx/logs/access.log \
	&& ln -sf /dev/stderr /usr/local/openresty/nginx/logs/error.log

CMD ["openresty", "-g", "daemon off;"]
