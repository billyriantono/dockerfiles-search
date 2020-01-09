FROM alpine:3.6
LABEL maintainer "KOBA789 <kobahide789@gmail.com>"

RUN set -x \
	&& apk upgrade --update \
	&& apk add \
		bash \
		'nodejs>=6.5.0' \
		nodejs-npm \
		coreutils \
		libusb \
		pcsc-lite \
		pcsc-lite-libs \
		curl \
		ca-certificates \
		util-linux \
	\
	&& apk add --virtual .build-deps \
		git \
		make \
		gcc \
		g++ \
		gzip \
		autoconf \
		automake \
		libc-dev \
		musl-dev \
		eudev-dev \
		libevent-dev \
		pcsc-lite-dev \
		linux-headers \
		libusb-dev \
	\
	&& npm install pm2 -g \
	\
	&& npm install arib-b25-stream-test -g --unsafe \
	\
	&& touch /usr/local/bin/update-rc.d ; chmod a+x /usr/local/bin/update-rc.d \
	&& npm install mirakurun -g --unsafe --production \
	&& mkdir -p /usr/local/share/mirakurun \
	\
	# recdvb
	&& git clone https://github.com/mzyy94/recdvb /tmp/recdvb \
	&& cd /tmp/recdvb \
	&& chmod +x ./autogen.sh \
	&& ./autogen.sh \
	&& ./configure \
	&& sed -i '/#include <sys\/msg.h>/d' recpt1core.h \
	&& sed -i -E 's!(#include <sys/msg.h>)!#undef _GNU_SOURCE\n#undef _BSD_SOURCE\n\1!' recpt1.c \
	&& sed -i -E 's!(#include <sys/msg.h>)!#undef _GNU_SOURCE\n#undef _BSD_SOURCE\n\1!' recpt1ctl.c \
	&& sed -i -E 's!(#include <sys/msg.h>)!#undef _GNU_SOURCE\n#undef _BSD_SOURCE\n\1!' checksignal.c \
	&& sed -i -E 's!(#include <ctype.h>)!\1\n#include <event.h>!' tssplitter_lite.c \
	&& sed -i 's#-I../driver#-I../driver -I/usr/local/include#' Makefile \
	&& make \
	&& make install \
	\
	# ccid
	&& cd /tmp \
	&& curl -s https://alioth.debian.org/frs/download.php/file/4205/ccid-1.4.26.tar.bz2 -o ccid-latest.tar.bz2 \
	&& tar xvf ccid-*.tar.bz2 \
	&& cd ccid-* \
	&& ./configure \
	&& make \
	&& make install \
	\
	# cleaning
	&& cd / \
	&& npm cache clean \
	&& apk del --purge .build-deps \
	&& rm -rf /tmp/* \
	&& rm -rf /var/cache/apk/*

	# forward request and error logs to docker log collector
	#&& ln -sf /dev/stdout /usr/local/var/log/mirakurun.stdout-0.log \
	#&& ln -sf /dev/stderr /usr/local/var/log/mirakurun.stderr-0.log

COPY services.sh /usr/local/bin
COPY conf/channels.yml /usr/local/etc/mirakurun/
COPY conf/server.yml /usr/local/etc/mirakurun/
COPY conf/tuners.yml /usr/local/etc/mirakurun/

WORKDIR /usr/lib/node_modules/mirakurun
CMD ["/usr/local/bin/services.sh"]
EXPOSE 40772
