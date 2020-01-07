FROM alpine:edge

# ensure local python is preferred over distribution python
ENV PATH /usr/local/bin:$PATH

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

# install ca-certificates so that HTTPS works consistently
# the other runtime dependencies for Python are installed later
RUN apk add --no-cache ca-certificates

ENV PYTHON_VERSION 2.7.13

ENV LIBRESSL_VERSION 2.4

# if this is called "PIP_VERSION", pip explodes with "ValueError: invalid truth value '<VERSION>'"
ENV PYTHON_PIP_VERSION 9.0.1


RUN apk add --no-cache clang clang-libs llvm llvm-libs alpine-sdk


ENV CC=clang
ENV CXX=clang++

RUN set -ex \
        && apk add --no-cache --update \
	        binutils \
		llvm \
		llvm-libs \
                clang \
		clang-libs \
		libressl \
                libressl$LIBRESSL_VERSION-libssl \
                libressl$LIBRESSL_VERSION-libtls \
                libressl$LIBRESSL_VERSION-libcrypto \
	&& apk add --no-cache --virtual .fetch-deps \
		gnupg \
		clang \
		llvm \
                libressl \
		tar \
		xz \
	\
	&& wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
	&& wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& wget -O pubkeys.txt "https://www.python.org/static/files/pubkeys.txt" \
	&& gpg --import pubkeys.txt \
	&& mkdir -p /usr/src/python \
	&& tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
	&& rm python.tar.xz \
	\
	&& apk add --no-cache --virtual .build-deps  \
		bzip2-dev \
		llvm-dev \
		clang-dev \
		gdbm-dev \
		libc-dev \
		linux-headers \
		make \
		ncurses-dev \
		libressl \
                libressl$LIBRESSL_VERSION-libssl \
                libressl$LIBRESSL_VERSION-libtls \
                libressl$LIBRESSL_VERSION-libcrypto \
		libressl-dev \
		pax-utils \
		readline-dev \
		sqlite-dev \
		tcl-dev \
		tk \
		tk-dev \
		zlib-dev \
		expat-dev \
	\
	&& apk del .fetch-deps \
	\
	&& cd /usr/src/python \
	&& ./configure \
		--enable-shared \
		--enable-unicode=ucs4 \
		--enable-ipv6 \
		--with-threads \
		--with-system-ffi \
		--with-system-expat \
		--with-system-zlib \
		CC=$CC CXX=$CXX \
		CFLAGS="-O3 -Qunused-arguments" CXXFLAGS="-O3" CPPFLAGS="-Qunused-arguments" CXXCPPFLAGS="-Qunused-arguments" \
	&& make -j$(getconf _NPROCESSORS_ONLN) \
	&& make install \
	\
		&& wget -O /tmp/get-pip.py 'https://bootstrap.pypa.io/get-pip.py' \
		&& python2 /tmp/get-pip.py "pip==$PYTHON_PIP_VERSION" \
		&& rm /tmp/get-pip.py \
	&& pip install --no-cache-dir --upgrade --force-reinstall "pip==$PYTHON_PIP_VERSION" \
	&& [ "$(pip list |tac|tac| awk -F '[ ()]+' '$1 == "pip" { print $2; exit }')" = "$PYTHON_PIP_VERSION" ] \
	\
	&& find /usr/local -depth \
		\( \
			\( -type d -a -name test -o -name tests \) \
			-o \
			\( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
		\) -exec rm -rf '{}' + \
	&& runDeps="$( \
		scanelf --needed --nobanner --recursive /usr/local \
			| awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
			| sort -u \
			| xargs -r apk info --installed \
			| sort -u \
	)" \
	&& apk add --virtual .python-rundeps $runDeps \
	&& apk del .build-deps \
	&& rm -rf /usr/src/python ~/.cache

CMD ["python2"]
