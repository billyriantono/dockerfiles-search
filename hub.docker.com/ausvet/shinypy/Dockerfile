# 3838
# /srv/shiny-server/
# /var/log/shiny-server/

FROM ausvet/shiny

# setup python
## install additional python
RUN apt-get install -y gpg\
    build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
    xz-utils tk-dev libffi-dev liblzma-dev \
    tar

ENV GPG_KEY 0D96DF4D4110E5C43FBFB17F2D347EA6AA65421D
ENV PYTHON_VERSION 3.7.3

RUN set -ex \
    && wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
    && wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
    && gpg --batch --verify python.tar.xz.asc python.tar.xz \
    && { command -v gpgconf > /dev/null && gpgconf --kill all || :; } \
    && rm -rf "$GNUPGHOME" python.tar.xz.asc \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
    && rm python.tar.xz

# install python
RUN cd /usr/src/python \
    && gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
    && ./configure \
    --build="$gnuArch" \
    --enable-loadable-sqlite-extensions \
    --enable-shared \
    --with-system-expat \
    --with-system-ffi \
    && make -j "$(nproc)" \
    && make altinstall \
    && ldconfig

# clean up the install
RUN find /usr/local -depth \
    \( \
    \( -type d -a \( -name test -o -name tests \) \) \
    -o \
    \( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
    \) -exec rm -rf '{}' + \
    && rm -rf /usr/src/python 

# remap python3 to the new python3
RUN rm /usr/bin/pdb3 \
    && rm /usr/bin/pydoc3 \
    && rm /usr/bin/pygettext3 \
    && rm /usr/bin/python3 \
    && rm /usr/bin/python3m

RUN sed -i "s/python3 -Es/python3.5 -Es/g" /usr/bin/lsb_release

RUN ln -s /usr/local/bin/pdb3.7 /usr/bin/pdb3 \
    && ln -s /usr/local/bin/pip3.7 /usr/bin/pip3 \
    && ln -s /usr/local/bin/pydoc3.7 /usr/bin/pydoc3 \
    && ln -s /usr/local/bin/pygettext3.7 /usr/bin/pygettext3 \
    && ln -s /usr/local/bin/python3.7 /usr/bin/python3 \
    && ln -s /usr/local/bin/python3.7m /usr/bin/python3m 

# install pipenv
RUN pip3 install -U pipenv

EXPOSE 3838

CMD ["/usr/bin/shiny-server.sh"]
