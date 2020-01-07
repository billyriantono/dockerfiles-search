FROM konmeo/minideb-dev

ENV PYTHON_VERSION 3.6.4

RUN install_packages \
        wget file xz-utils \
        libbz2-dev libc6-dev libexpat1-dev libffi-dev libgdbm-dev \
        liblzma-dev libmpdec-dev libncursesw5-dev libreadline-dev \
        libsqlite3-dev libssl-dev zlib1g-dev

RUN wget -q https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz -O- | tar zxf -

WORKDIR /workdir/Python-$PYTHON_VERSION

ENV CONFIG_PARAMS='\
        --enable-optimizations --with-lto \
        --enable-loadable-sqlite-extensions \
        --with-dbmliborder=bdb:gdbm --with-computed-gotos --without-ensurepip \
        --with-system-expat --with-system-libmpdec --with-system-ffi --with-fpectl' \
    LANG='C.UTF-8'

RUN ./configure --enable-shared $CONFIG_PARAMS
RUN make
RUN make install

RUN make distclean

RUN ./configure $CONFIG_PARAMS
RUN make
RUN make altbininstall

RUN cp -r /usr/local/lib /usr/local/lib2 && \
    find /usr/local/lib2/python3.6/test/* -not -name pystone.py -exec rm -rf '{}' + && \
    find /usr/local/lib2 -type d \( -name 'pkgconfig' -o -name 'config-*' \) -exec rm -rf '{}' + && \
    find /usr/local/lib2 -type f \( -name '*.pyc' -o -name '*.a' \) -exec rm -f '{}' +
