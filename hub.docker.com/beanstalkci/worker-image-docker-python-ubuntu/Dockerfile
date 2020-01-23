# =====
# SETUP
# =====

FROM buildpack-deps:jessie
ENV PATH /usr/local/bin:$PATH

# If this is called "PIP_VERSION", pip explodes with "ValueError: invalid truth value '<VERSION>'"
ENV PYTHON_PIP_VERSION 9.0.1
ENV LANG C.UTF-8

# Install Dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends tcl tk dpkg-dev tcl-dev tk-dev \
    && rm -rf /var/lib/apt/lists/*

# Download get-pip.py
RUN set -ex \
    && wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py'


# PYTHON 3.6.1
# ------------
# See: https://github.com/docker-library/python/blob/88ba87d31a3033d4dbefecf44ce25aa1b69ab3e5/3.6/Dockerfile


ENV PYTHON python3.6
ENV PYTHON_MAJOR_VERSION 3.6
ENV PYTHON_VERSION 3.6.1
ENV GPG_KEY 0D96DF4D4110E5C43FBFB17F2D347EA6AA65421D

# Install Python
RUN set -ex \
    && wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
    && wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
    && gpg --batch --verify python.tar.xz.asc python.tar.xz \
    && rm -rf "$GNUPGHOME" python.tar.xz.asc \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
    && rm python.tar.xz \
    && cd /usr/src/python \
    && ./configure \
         --build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	 --enable-loadable-sqlite-extensions \
	 --enable-shared \
	 --with-system-expat \
	 --with-system-ffi \
	 --without-ensurepip \
    && make -j "$(nproc)" \
    && make install \
    && ldconfig \
    && rm -rf /usr/src/python

# Make some useful symlinks that are expected to exist
RUN cd /usr/local/bin \
    && ln -s idle3 idle \
    && ln -s pydoc3 pydoc \
    && ln -s python3 python \
    && ln -s python3-config python-config

# Install Pip
RUN set -ex \
    && $PYTHON get-pip.py \
        --disable-pip-version-check \
        --no-cache-dir \
        "pip==$PYTHON_PIP_VERSION"
RUN $PYTHON -m pip install --no-cache-dir -U pip
RUN $PYTHON -m pip install --no-cache-dir virtualenv


# PYTHON 3.5.3
# ------------
# See: https://github.com/docker-library/python/blob/88ba87d31a3033d4dbefecf44ce25aa1b69ab3e5/3.5/Dockerfile


ENV PYTHON python3.5
ENV PYTHON_MAJOR_VERSION 3.5
ENV PYTHON_VERSION 3.5.3
ENV GPG_KEY 97FC712E4C024BBEA48A61ED3A5CA953F73C700D

# Install Python
RUN set -ex \
    && wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
    && wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
    && gpg --batch --verify python.tar.xz.asc python.tar.xz \
    && rm -rf "$GNUPGHOME" python.tar.xz.asc \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
    && rm python.tar.xz \
    && cd /usr/src/python \
    && ./configure \
         --build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	 --enable-loadable-sqlite-extensions \
	 --enable-shared \
	 --with-system-expat \
	 --with-system-ffi \
	 --without-ensurepip \
    && make -j "$(nproc)" \
    && make install \
    && ldconfig \
    && rm -rf /usr/src/python

# Install Pip
RUN set -ex \
    && $PYTHON get-pip.py \
        --disable-pip-version-check \
        --no-cache-dir \
        "pip==$PYTHON_PIP_VERSION"
RUN $PYTHON -m pip install --no-cache-dir -U pip
RUN $PYTHON -m pip install --no-cache-dir virtualenv


# PYTHON 3.4.6
# ------------
# See: https://github.com/docker-library/python/blob/88ba87d31a3033d4dbefecf44ce25aa1b69ab3e5/3.4/Dockerfile


ENV PYTHON python3.4
ENV PYTHON_MAJOR_VERSION 3.4
ENV PYTHON_VERSION 3.4.6
ENV GPG_KEY 97FC712E4C024BBEA48A61ED3A5CA953F73C700D

# Install Python
RUN set -ex \
    && wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
    && wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
    && gpg --batch --verify python.tar.xz.asc python.tar.xz \
    && rm -rf "$GNUPGHOME" python.tar.xz.asc \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
    && rm python.tar.xz \
    && cd /usr/src/python \
    && ./configure \
         --build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	 --enable-loadable-sqlite-extensions \
	 --enable-shared \
	 --with-system-expat \
	 --with-system-ffi \
	 --without-ensurepip \
    && make -j "$(nproc)" \
    && make install \
    && ldconfig \
    && rm -rf /usr/src/python

# Install Pip
RUN set -ex \
    && $PYTHON get-pip.py \
        --disable-pip-version-check \
        --no-cache-dir \
        "pip==$PYTHON_PIP_VERSION"
RUN $PYTHON -m pip install --no-cache-dir -U pip
RUN $PYTHON -m pip install --no-cache-dir virtualenv


# PYTHON 3.3.6
# ------------
# See: https://github.com/docker-library/python/blob/1ca4a57b20a2f66328e5ef72df866f701c0cd306/3.3/Dockerfile


ENV PYTHON python3.3
ENV PYTHON_MAJOR_VERSION 3.3
ENV PYTHON_VERSION 3.3.6
ENV GPG_KEY 26DEA9D4613391EF3E25C9FF0A5B101836580288

# Install Python
RUN set -ex \
    && wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
    && wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
    && gpg --batch --verify python.tar.xz.asc python.tar.xz \
    && rm -rf "$GNUPGHOME" python.tar.xz.asc \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
    && rm python.tar.xz \
    && cd /usr/src/python \
    && ./configure \
         --build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	 --enable-loadable-sqlite-extensions \
	 --enable-shared \
	 --with-system-expat \
	 --with-system-ffi \
	 --without-ensurepip \
    && make -j "$(nproc)" \
    && make install \
    && ldconfig \
    && rm -rf /usr/src/python

# Install Pip
RUN set -ex \
    && $PYTHON get-pip.py \
        --disable-pip-version-check \
        --no-cache-dir \
        "pip==$PYTHON_PIP_VERSION"
RUN $PYTHON -m pip install --no-cache-dir -U pip
RUN $PYTHON -m pip install --no-cache-dir virtualenv


# PYTHON 2.7.13
# -------------
# See: https://github.com/docker-library/python/blob/1ca4a57b20a2f66328e5ef72df866f701c0cd306/2.7/Dockerfile


ENV PYTHON_MAJOR_VERSION 2.7
ENV PYTHON_VERSION 2.7.13
ENV PYTHON python2.7
ENV GPG_KEY C01E1CAD5EA2C4F0B8E3571504C367C218ADD4FF

# Install Python
RUN set -ex \
    && wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
    && wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
    && gpg --batch --verify python.tar.xz.asc python.tar.xz \
    && rm -rf "$GNUPGHOME" python.tar.xz.asc \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
    && rm python.tar.xz \
    && cd /usr/src/python \
    && ./configure \
        --build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
        --enable-shared \
        --enable-unicode=ucs4 \
    && make -j "$(nproc)" \
    && make install \
    && ldconfig \
    && rm -rf /usr/src/python

# Install Pip
RUN set -ex \
    && $PYTHON get-pip.py \
        --disable-pip-version-check \
        --no-cache-dir \
        "pip==$PYTHON_PIP_VERSION"
RUN $PYTHON -m pip install --no-cache-dir -U pip
RUN $PYTHON -m pip install --no-cache-dir virtualenv

# Remove all .pyc and .pyo files
RUN set -ex \
    && find /usr/local -depth \
        \( \
            \( -type d -a -name test -o -name tests \) \
            -o \
            \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        \) -exec rm -rf '{}' +

# Remove get-pip.py
RUN rm -f get-pip.py

# Remove installation dependencies
RUN apt-get purge -y --auto-remove $PYTHON_BUILD_DEPS \
    && rm -rf /var/lib/apt/lists/*
