FROM debian:stable

COPY /dependencies/ /opt/deps

RUN apt update && apt upgrade --yes && \
	apt install --no-install-recommends --yes \
	git curl ca-certificates nano zip unzip tar xz-utils cmake g++ make pkg-config \
	libtool-bin autoconf automake build-essential cmake pkg-config pcsc-tools pcscd \
	libpcsclite1  python-dev virtualenv libudev-dev libboost-all-dev libreadline-dev

RUN mkdir -p /opt/cache 																																																	&& \
	tar xJf /opt/deps/zlib.tar.xz 		-C /opt/cache 																																										&& \
	tar xJf /opt/deps/openssl.tar.xz 	-C /opt/cache 																																										&& \
	tar xJf /opt/deps/libsodium.tar.xz 	-C /opt/cache 																																										&& \
	tar xJf /opt/deps/libzmq.tar.xz 	-C /opt/cache 																																										&& \
	tar xJf /opt/deps/cppzmq.tar.xz 	-C /opt/cache 																																										&& \
	tar xJf /opt/deps/curl.tar.xz 		-C /opt/cache 																																										&& \
	tar xJf /opt/deps/usb.tar.xz 		-C /opt/cache 																																										&& \
	tar xJf /opt/deps/hidapi.tar.xz 	-C /opt/cache 																																										&& \
	cd /opt/cache/zlib 		&& 					./configure --static --prefix=/usr 																													&& make && make install && \
	cd /opt/cache/openssl 	&& 					./Configure --static --prefix=/usr --with-zlib-include=/usr/include --with-zlib-lib=/usr/lib linux-x86_64 no-asm no-shared 							&& make && make install && \
	cd /opt/cache/libsodium && ./autogen.sh && 	./configure --disable-soname-versions --enable-shared=no --enable-static=yes --prefix=/usr 															&& make && make install && \
	cd /opt/cache/libzmq	&& ./autogen.sh && 	./configure --without-docs --disable-curve-keygen --enable-libunwind=no --enable-shared=no --enable-static=yes --with-libsodium=yes --prefix=/usr 	&& make && make install && \
	cd /opt/cache/usb 		&& ./autogen.sh && 	CFLAGS="-fPIC" CXXFLAGS="-fPIC" ./configure --prefix=/usr --enable-static --disable-shared 															&& make && make install && \
	cd /opt/cache/hidapi 	&& ./bootstrap  && 	CFLAGS="-fPIC" CXXFLAGS="-fPIC" ./configure --prefix=/usr --enable-static --disable-shared 															&& make && make install && \
	cd /opt/cache/curl 		&& 					LIBS="-ldl -lpthread" ./configure --prefix=/usr --without-ssl --without-zlib --disable-dict --disable-ftp --disable-gopher --disable-file 									   \
		--disable-imap --disable-ldap --disable-ldaps --disable-pop3 --disable-proxy --disable-rtsp --disable-smtp --disable-telnet --disable-tftp --disable-smb --disable-smbs 											   \
		--without-nghttp2 --disable-psl --without-brotli --without-libidn2 --without-libpsl --without-librtmp --enable-static --disable-shared 														&& make && make install && \
	cp /opt/cache/cppzmq/zmq.hpp /usr/include/zmq.hpp 																																										&& \
	cp /opt/cache/cppzmq/zmq_addon.hpp /usr/include/zmq_addon.hpp 																																							&& \
	cp -r /opt/cache/curl/include/curl /usr/include 																																										&& \
	rm -rf /opt/cache && rm -rf /opt/deps

	VOLUME ["/code"]
