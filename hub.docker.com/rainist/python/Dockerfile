FROM centos:7.6.1810

LABEL maintainer="Rainist Engineering <engineering@rainist.com>"

RUN yum install -y \
        gcc \
        make \
        openssl-devel \
        bzip2-devel \
        libffi-devel \
        sqlite-devel \
        python3-dev \
        ncurses-devel \
        wget \
    && yum clean all \
    && rm -rf /var/cache/yum

ENV PATH /usr/local/bin:$PATH

ENV PYTHON_VERSION 3.7.5

RUN set -ex \
    && wget -q https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz \
    && tar xzf Python-${PYTHON_VERSION}.tgz \
    && cd Python-${PYTHON_VERSION} \
    && ./configure \
        --enable-optimizations \
        --enable-loadable-sqlite-extensions \
        --with-system-ffi \
        --without-ensurepip \
    && make -j "$(nproc)" \
    && make altinstall \
    && ldconfig \
    && cd .. && rm -rf Python-${PYTHON_VERSION}*

RUN cd /usr/local/bin \
    && ln -s idle3.7 idle \
    && ln -s pydoc3.7 pydoc \
    && ln -s python3.7 python \
    && ln -s python3.7 python3 \
    && ln -s python3.7m-config python-config \
    && ln -s pyvenv-3.7 pyvenv

ENV PYTHON_PIP_VERSION 19.1.1

RUN wget -q -O get-pip.py "https://bootstrap.pypa.io/get-pip.py" \
    && python get-pip.py \
        --disable-pip-version-check \
        --no-cache-dir \
        "pip==$PYTHON_PIP_VERSION" \
    && rm -f get-pip.py \
    && pip --version

CMD ["python3"]
