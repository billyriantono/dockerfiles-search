FROM alpine:3.10 AS source
RUN apk update
RUN apk add \
	coreutils \
	git \
	ca-certificates \
	tar \
	xz \
	autoconf \
	dpkg \
	file \
	g++ \
	gcc \
	bison \
	make \
	pkgconf \
	re2c
RUN git clone https://github.com/php/php-src.git /src/php
RUN git clone https://github.com/php-fig/container.git /src/container
RUN git clone https://github.com/php-fig/log.git /src/log
RUN git -C /src/php checkout PHP-7.4
RUN cd /src/php && ./buildconf --force
RUN apk add \
	dpkg-dev \
	musl-dev \
	argon2-dev \
	ncurses-dev \
	ncurses-static \
	libevent-dev \
	libevent-static \
	libsodium-dev \
	libsodium-static \
	libxml2-dev \
	openssl-dev \
	sqlite-dev \
	sqlite-static \
	libpng-dev \
	libpng-static \
	libjpeg-turbo-dev \
	libwebp-dev \
	libxpm-dev \
	icu-dev \
	icu-static \
	oniguruma-dev \
	gnu-libiconv-dev
RUN cd /src/php && \
	CFLAGS="-fstack-protector-strong -fpic -fpie -pie -O2 -Wl,-static,-zmuldefs,-O2,--hash-style=both,--strip-all -static -static-libgcc -l:libstdc++.a -l:libargon2.a -l:libpng16.a -l:libxml2.a -l:libicuio.a -l:libicui18n.a -l:libicuuc.a -l:libsodium.a" \
	CPPFLAGS="-fstack-protector-strong -fpic -fpie -pie -O2 -Wl,-static,-zmuldefs,-O2,--hash-style=both,--strip-all -static -static-libgcc -static-libstdc++ -l:libargon2.a -l:libpng16.a -l:libxml2.a -l:libicuio.a -l:libicui18n.a -l:libicuuc.a -l:libsodium.a" \
	LDFLAGS="-Wl,-static,-zmuldefs,-O2,--hash-style=both,--strip-all -fpic -fpie -pie -static -static-libgcc" \
	./configure \
		--build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
		--prefix=/ \
		--bindir=/lib \
		--libdir=/lib \
		--sbindir=/lib \
		--libexecdir=/lib \
		--sysconfdir=/etc \
		--runstatedir=/tmp \
		--with-config-file-path=/etc \
		--with-config-file-scan-dir=/etc/conf.d \
		--enable-option-checking=fatal \
		--disable-rpath \
		--disable-shared \
		--enable-fpm \
		--enable-static \
		--enable-static=opcache \
		--enable-intl \
		--enable-sockets \
		--enable-ftp \
		--enable-mbstring \
		--enable-mysqlnd \
		--enable-opcache \
		--enable-pcntl \
		--enable-gd \
		--with-layout=GNU \
		--with-mhash \
		--with-password-argon2 \
		--with-sodium \
		--with-openssl \
		--with-zlib \
		--with-mysqli \
		--disable-cli \
		--disable-cgi \
		--disable-phpdbg \
		--disable-phar \
		--disable-pdo \
		--disable-short-tags \
		--without-curl \
		--without-pear \
		--without-readline
RUN make -C /src/php -j "$(nproc)"
RUN make -C /src/php -j "$(nproc)" install
RUN mkdir -p /dest/lib /dest/files /dest/tmp /dest/etc/conf.d /dest/Psr/Log /dest/Psr/Container
RUN cp /lib/ld-musl-x86_64.so.1 /dest/lib/
RUN cp /lib/php-fpm /dest/lib/
RUN cp /src/php/php.ini-production /dest/etc/php.ini
RUN cp /src/log/Psr/Log/*.php /dest/Psr/Log/
RUN cp /src/container/src/*.php /dest/Psr/Container
COPY config/php-fpm.conf /dest/etc/php-fpm.conf
COPY assets /dest/assets
COPY src /dest/DaveKok
RUN find /dest/

FROM scratch
COPY --from=source /dest/ /
EXPOSE 9000
WORKDIR /
STOPSIGNAL SIGQUIT
ENTRYPOINT ["/lib/php-fpm"]
