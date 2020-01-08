FROM tozd/base:ubuntu-xenial

# Prevent Python packages to be installed through APT.
COPY ./etc/apt /etc/apt

# General dependencies for building dependencies and locales.
RUN sed -i 's/^# deb-src/deb-src/' /etc/apt/sources.list && \
 apt-get update -q -q && \
 apt-get install --yes --force-yes --no-install-recommends swig git build-essential cmake wget ssh tar gzip ca-certificates && \
 locale-gen --no-purge en_US.UTF-8 && \
 update-locale LANG=en_US.UTF-8 && \
 echo locales locales/locales_to_be_generated multiselect en_US.UTF-8 UTF-8 | debconf-set-selections && \
 echo locales locales/default_environment_locale select en_US.UTF-8 | debconf-set-selections && \
 dpkg-reconfigure locales

# Docker.
RUN apt-get update -q -q && \
 apt-get install --yes --force-yes apt-transport-https ca-certificates curl && \
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
 echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable" > /etc/apt/sources.list.d/docker.list && \
 apt-get update -q -q && \
 apt-get install --yes --force-yes docker-ce

# Set locale to UTF-8 which makes Python read text in UTF-8 and not ASCII, but default.
ENV LC_ALL=en_US.UTF-8

# apt-get build-dep python3 without Python itself.
RUN apt-get install --yes --force-yes --no-install-recommends autotools-dev bsdmainutils debhelper debiandoc-sgml \
 dh-strip-nondeterminism distro-info-data docutils-common file gettext gettext-base groff-base intltool-debian \
 libarchive-zip-perl libasprintf0v5 libcroco3 libfile-stripnondeterminism-perl libglib2.0-0 libhtml-parser-perl \
 libhtml-tagset-perl libmagic1 libmpdec2 libosp5 libpipeline1 libroman-perl libsgmls-perl libtext-format-perl \
 libtimedate-perl libunistring0 liburi-perl man-db mime-support opensp po-debconf sgml-data sgmlspl

# Extra Python dependencies.
RUN apt-get install --yes --force-yes --no-install-recommends zlib1g-dev libexpat1-dev tk8.6-dev libffi-dev libssl-dev \
 libbz2-dev liblzma-dev libncurses5-dev libreadline6-dev libsqlite3-dev libgdbm-dev liblzma-dev lzma lzma-dev

# Compiling Python 3.6.
RUN cd /usr/src && \
 wget --quiet https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz && \
 tar xzf Python-3.6.3.tgz && \
 cd Python-3.6.3 && \
 ./configure --enable-optimizations --enable-shared --enable-loadable-sqlite-extensions --with-system-expat --with-system-ffi --enable-ipv6 && \
 make -j8 install && \
 ldconfig && \
 rm -rf /usr/src/*
