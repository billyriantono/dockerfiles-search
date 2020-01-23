FROM alpine

RUN set -eux; \
	\
	sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories; \
	sed -i 's/uk.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories; \
	apk --no-cache --no-progress upgrade; \
	buildDeps=' \
		build-base \
		automake \
		libtool \
		m4 \
		autoconf \
		git \
		linux-headers \
	'; \
	apk add --no-cache --virtual .build-deps \
		$buildDeps \
	;

RUN set -eux; \
	cd /opt; \
	libuv_version="1.32.0"; \
	wget https://github.com/libuv/libuv/archive/v$libuv_version.tar.gz -Olibuv-$libuv_version.tar.gz; \
	tar xvf libuv-$libuv_version.tar.gz; \
	cd libuv-$libuv_version; \
	./autogen.sh; \
	./configure --prefix=/opt/libuv --enable-shared=no --enable-static=yes CC="gcc -O3"; \
	make -j4; \
	make install; \
	\
	cd ..; \
	git clone https://github.com/zfl9/dns2tcp; \
	cd dns2tcp; \
	make -j4 INCLUDES="-I/opt/libuv/include" LDFLAGS="-L/opt/libuv/lib"; \
	make install; \
	\
	# ip2socks
	cd ..; \
	git clone https://github.com/zfl9/ipt2socks; \
	cd ipt2socks; \
	make -j4 INCLUDES="-I/opt/libuv/include" LDFLAGS="-L/opt/libuv/lib";\ 
	make install;
