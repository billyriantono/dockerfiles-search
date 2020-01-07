FROM alpine:3.10

# ensure local python is preferred over distribution python
ARG PATH=/usr/local/bin:$PATH

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ARG LANG=C.UTF-8

# install ca-certificates so that HTTPS works consistently
# other runtime dependencies for Python are installed later
RUN apk add --no-cache ca-certificates

ARG GPG_KEY=0D96DF4D4110E5C43FBFB17F2D347EA6AA65421D

ARG PYTHON_VERSION36=3.6.9

ARG PYTHON_VERSION37=3.7.5

RUN set -ex \
	&& apk add --no-cache --virtual .fetch-deps \
		gnupg \
		tar \
		xz \
	\
	######### add version python #########

	&& wget -O python37.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION37%%[a-z]*}/Python-$PYTHON_VERSION37.tar.xz" \
    && wget -O python37.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION37%%[a-z]*}/Python-$PYTHON_VERSION37.tar.xz.asc" \

	&& wget -O python36.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION36%%[a-z]*}/Python-$PYTHON_VERSION36.tar.xz" \
	&& wget -O python36.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION36%%[a-z]*}/Python-$PYTHON_VERSION36.tar.xz.asc" \


    ######### end #############

	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \

	&& gpg --batch --verify python37.tar.xz.asc python37.tar.xz \
	&& gpg --batch --verify python36.tar.xz.asc python36.tar.xz \

	&& { command -v gpgconf > /dev/null && gpgconf --kill all || :; } \

	&& rm -rf "$GNUPGHOME" python37.tar.xz.asc \
    && rm -rf "$GNUPGHOME" python36.tar.xz.asc \

	&& mkdir -p /usr/src/python3.7 \
	&& tar -xJC /usr/src/python3.7 --strip-components=1 -f python37.tar.xz \

	&& mkdir -p /usr/src/python3.6 \
	&& tar -xJC /usr/src/python3.6 --strip-components=1 -f python36.tar.xz \

	&& rm python37.tar.xz \
	&& rm python36.tar.xz

RUN apk add --no-cache --virtual .build-deps  \
		bzip2-dev \
		coreutils \
		dpkg-dev dpkg \
		expat-dev \
		findutils \
		gcc \
		gdbm-dev \
		libc-dev \
		libffi-dev \
		libnsl-dev \
		libtirpc-dev \
		linux-headers \
		make \
		ncurses-dev \
		openssl-dev \
		pax-utils \
		readline-dev \
		sqlite-dev \
		tcl-dev \
		tk \
		tk-dev \
		xz-dev \
		zlib-dev

# add build deps before removing fetch deps in case there's overlap
RUN apk del .fetch-deps \
	\
	&& cd /usr/src/python3.7 \
    && gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
    && ./configure \
    	--build="$gnuArch" \
    	--enable-loadable-sqlite-extensions \
    	--enable-shared \
    	--with-system-expat \
    	--with-system-ffi \
    	--without-ensurepip \
    && make -j "$(nproc)" \
    && make install \
	&& cd /usr/src/python3.6 \
	&& gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	&& ./configure \
		--build="$gnuArch" \
		--enable-loadable-sqlite-extensions \
		--enable-shared \
		--with-system-expat \
		--with-system-ffi \
		--without-ensurepip \
	&& make -j "$(nproc)" \
	&& make install

# make some useful symlinks that are expected to exist
RUN cd /usr/local/bin \
	&& ln -s idle3 idle \
	&& ln -s pydoc3 pydoc \
	&& ln -s python3 python \
	&& ln -s python3-config python-config

# if this is called "PIP_VERSION", pip explodes with "ValueError: invalid truth value '<VERSION>'"
ARG PYTHON_PIP_VERSION=19.3.1
# https://github.com/pypa/get-pip
ARG PYTHON_GET_PIP_URL=https://github.com/pypa/get-pip/raw/ffe826207a010164265d9cc807978e3604d18ca0/get-pip.py
ARG PYTHON_GET_PIP_SHA256=b86f36cc4345ae87bfd4f10ef6b2dbfa7a872fbff70608a1e43944d283fd0eee

RUN set -ex; \
	\
	wget -O get-pip.py "$PYTHON_GET_PIP_URL"; \
	echo "$PYTHON_GET_PIP_SHA256 *get-pip.py" | sha256sum -c -; \
	\
	/usr/local/bin/python3 get-pip.py \
		--disable-pip-version-check \
		--no-cache-dir \
		"pip==$PYTHON_PIP_VERSION" \
	; \
	pip --version;

RUN find /usr/local -depth \
		\( \
			\( -type d -a \( -name test -o -name tests -o -name idle_test \) \) \
			-o \
			\( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
		\) -exec rm -rf '{}' +; \
	rm -f get-pip.py

CMD ["python3"]
