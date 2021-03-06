FROM library/debian:jessie

#
# mostly copy/pasta from the Dockerfile here: https://registry.hub.docker.com/u/library/python/
# the official repo is almost 800mb because of all the crap it installs on top of debian:jessie
# ...buildpack-deps:jessie, buildpack-deps:jessie-curl, buildpack-deps:jessie-scm
#
# NOTE: if you want to use something like lxml, gevent, psycopg2, you will need to install the
# appropriate os lib (libxml2-dev, libevent-dev, libpq-dev, etc)
#

# remove several traces of debian python
RUN apt-get purge -y python.*

RUN apt-get update && apt-get -y install \
    curl \
    gcc \
    perl \
    make \
    git \
    openssh-client \
    xz-utils

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

ENV PYTHON_VERSION 3.4.3

# gpg: key F73C700D: public key "Larry Hastings <larry@hastings.org>" imported
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 97FC712E4C024BBEA48A61ED3A5CA953F73C700D

RUN set -x \
    && mkdir -p /usr/src/python \
    && curl -SL "https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tar.xz" -o python.tar.xz \
    && curl -SL "https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tar.xz.asc" -o python.tar.xz.asc \
    && gpg --verify python.tar.xz.asc \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
    && rm python.tar.xz* \
    && cd /usr/src/python \
    && ./configure --enable-shared --enable-unicode=ucs4 \
    && make -j$(nproc) \
    && make install \
    && ldconfig \
    && find /usr/local \
        \( -type d -a -name test -o -name tests \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' + \
    && rm -rf /usr/src/python

# make some useful symlinks that are expected to exist
RUN cd /usr/local/bin \
    && ln -s easy_install-3.4 easy_install \
    && ln -s idle3 idle \
    && ln -s pip3 pip \
    && ln -s pydoc3 pydoc \
    && ln -s python3 python \
    && ln -s python-config3 python-config

CMD ["python3"]
