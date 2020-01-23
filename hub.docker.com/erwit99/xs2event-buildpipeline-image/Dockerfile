FROM python:3.7-slim
LABEL Description="Python BUILD" Vendor="xs2event" Version="1.0"
ENV VIRTUALENV="/opt/venv"
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    curl \
    nano \
    nginx \
    lsof \
    make \
    wget \
    python3 \
    git \
    python3-distutils \
 && rm -rf /var/lib/apt/lists/*

RUN ln -snf /usr/bin/python3 /usr/bin/python
ENV PYTHON_PIP_VERSION 19.3.1
RUN set -ex; \
    wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py'; \
    \
    python get-pip.py \
        --disable-pip-version-check \
        --no-cache-dir \
        "pip==$PYTHON_PIP_VERSION" \
    ; \
    pip --version; \
    \
    find /usr/local -depth \
        \( \
            \( -type d -a \( -name test -o -name tests \) \) \
            -o \
            \( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
        \) -exec rm -rf '{}' +; \
    rm -f get-pip.py

RUN set -ex; \
    curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs npm

RUN set -ex \
    && buildDeps=" \
        dpkg-dev \
        gcc \
        libbz2-dev \
        libc6-dev \
        libexpat1-dev \
        libffi-dev \
        libgdbm-dev \
        liblzma-dev \
        libncursesw5-dev \
        libreadline-dev \
        libsqlite3-dev \
        libssl-dev \
        tcl-dev \
        tk-dev \
        wget \
        xz-utils \
        zlib1g-dev \
        python3-dev \
        libxml2-dev \
        libxslt1-dev \
        netbase \
    " \
    && apt-get update && apt-get install -y $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
    && gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
    && pip install virtualenv \
    && virtualenv -p python3.7 ${VIRTUALENV} \
    && ANSIBLE_VERSION=2.8.7 \
    && /opt/venv/bin/pip3 install ansible==${ANSIBLE_VERSION} \
    && /opt/venv/bin/pip3 install safety \
    && /opt/venv/bin/pip3 install pytest \
    && /opt/venv/bin/pip3 install pytest_mock \
    && /opt/venv/bin/pip3 install mongomock \
    && /opt/venv/bin/pip3 install tox \
    && /opt/venv/bin/pip3 install cffi \
    && apt-get purge -y --auto-remove $buildDeps \
    \
    && find /usr/local -depth \
        \( \
            \( -type d -a \( -name test -o -name tests \) \) \
            -o \
            \( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
        \) -exec rm -rf '{}' +

ENV PATH "${VIRTUALENV}/bin:/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
RUN mkdir -p /root/.ssh && mkdir -p /opt/scripts/
COPY merge.sh /opt/scripts
RUN chmod +x /opt/scripts/merge.sh
COPY config.bitbucket /root/.ssh/config
COPY protocols.bitbucket /etc/protocols
RUN ln -snf /usr/local/bin/python3.7 /usr/bin/python
