# download hinkelsteinli alpine latest docker image
FROM hinkelsteinli/alpine:latest

# env variables
ENV PATH /usr/local/bin:$PATH
ENV GPG_KEY 0D96DF4D4110E5C43FBFB17F2D347EA6AA65421D
ENV PYTHON_VERSION 3.7.3

# install ca-certs to use https
RUN apk add --no-cache ca-certificates

# install packages to verify and extract python download
RUN set -ex && \
    apk add --no-cache --virtual .fetch-deps \
	gnupg \
	tar \
	xz && \ 
    # download python sourcecode and gpg check file
    wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" && \
    wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" && \
    # check download with gpg file and extract
    export GNUPGHOME="$(mktemp -d)" && \
    gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" && \
    gpg --batch --verify python.tar.xz.asc python.tar.xz && \
    { command -v gpgconf > /dev/null && gpgconf --kill all || :; } && \
    rm -rf "$GNUPGHOME" python.tar.xz.asc && \
    mkdir -p /usr/src/python && \
    tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz && \
    rm python.tar.xz && \
    # install depencies for compile python into virtual env
    apk add --no-cache --virtual .build-deps  \
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
	util-linux-dev \
	xz-dev \
	zlib-dev && \
    \
    apk del .fetch-deps && \
    # compile python
    cd /usr/src/python && \
    gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" && \
    ./configure \
	--build="$gnuArch" \
	--enable-loadable-sqlite-extensions \
	--enable-shared \
	--with-system-expat \
	--with-system-ffi \
	--without-ensurepip && \
    make -j "$(nproc)" \
	EXTRA_CFLAGS="-DTHREAD_STACK_SIZE=0x100000" && \
    make install && \
    find /usr/local -type f -executable -not \( -name '*tkinter*' \) -exec scanelf --needed --nobanner --format '%n#p' '{}' ';' \
	| tr ',' '\n' \
	| sort -u \
	| awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
	| xargs -rt apk add --no-cache --virtual .python-rundeps && \
    # delete not needed apk packages
    apk del .build-deps && \
    \
    find /usr/local -depth \
	\( \
	\( -type d -a \( -name test -o -name tests \) \) \
	-o \
	\( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
	\) -exec rm -rf '{}' + && \
    # delete source folder
    rm -rf /usr/src/python && \
    # check if python works
    python3 --version
# make some symlinks
RUN cd /usr/local/bin && \
    ln -s idle3 idle && \
    ln -s pydoc3 pydoc && \
    ln -s python3 python && \
    ln -s python3-config python-config

# env variables for python pip
ENV PYTHON_PIP_VERSION 19.0.3

# install python pip 
RUN set -ex; \
    wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py'; \
    python get-pip.py \
	--disable-pip-version-check \
	--no-cache-dir \
	"pip==$PYTHON_PIP_VERSION" \
    ; \
    pip --version; \
    find /usr/local -depth \
	\( \
	\( -type d -a \( -name test -o -name tests \) \) \
	-o \
	\( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
	\) -exec rm -rf '{}' +; \
    rm -f get-pip.py

# run python
CMD ["python"]
