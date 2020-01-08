# Copyright (C) The Arvados Authors. All rights reserved.
#
# SPDX-License-Identifier: AGPL-3.0

FROM debian:9

ENV DEBIAN_FRONTEND noninteractive

#RUN apt-get update && \
#    apt-get -yq --no-install-recommends -o Acquire::Retries=6 install \
#    postgresql-9.6 git build-essential runit curl libpq-dev \
#    libcurl4-openssl-dev libssl1.0-dev zlib1g-dev libpcre3-dev \
#    openssh-server python-setuptools netcat-traditional \
#    python-epydoc graphviz bzip2 less sudo virtualenv \
#    libpython-dev fuse libfuse-dev python-pip python-yaml \
#    pkg-config libattr1-dev python-llfuse python-pycurl \
#    libwww-perl libio-socket-ssl-perl libcrypt-ssleay-perl \
#    libjson-perl nginx gitolite3 lsof libreadline-dev \
#    apt-transport-https ca-certificates slurm-wlm \
#    linkchecker python3-virtualenv python-virtualenv xvfb iceweasel \
#    libgnutls28-dev python3-dev vim cadaver cython gnupg dirmngr \
#    libsecret-1-dev r-base r-cran-testthat libxml2-dev pandoc && \
#    apt-get clean

RUN apt-get update && \
    apt-get -yq --no-install-recommends -o Acquire::Retries=6 install \
    git build-essential curl \
    libcurl4-openssl-dev libssl1.0-dev zlib1g-dev libpcre3-dev \
    openssh-server python-setuptools netcat-traditional \
    python-epydoc graphviz bzip2 less sudo virtualenv \
    libpython-dev fuse libfuse-dev python-pip python-yaml \
    pkg-config libattr1-dev python-llfuse python-pycurl \
    libwww-perl libio-socket-ssl-perl libcrypt-ssleay-perl \
    libjson-perl gitolite3 lsof libreadline-dev \
    apt-transport-https ca-certificates slurm-wlm \
    linkchecker python3-virtualenv python-virtualenv xvfb iceweasel \
    libgnutls28-dev python3-dev cadaver cython gnupg dirmngr \
    libsecret-1-dev r-base r-cran-testthat libxml2-dev pandoc && \
    apt-get clean

ENV RUBYVERSION_MINOR 2.3
ENV RUBYVERSION 2.3.5

# Install Ruby from source
RUN cd /tmp && \
 curl -f http://cache.ruby-lang.org/pub/ruby/${RUBYVERSION_MINOR}/ruby-${RUBYVERSION}.tar.gz | tar -xzf - && \
 cd ruby-${RUBYVERSION} && \
 ./configure --disable-install-doc && \
 make && \
 make install && \
 cd /tmp && \
 rm -rf ruby-${RUBYVERSION}

ENV GEM_HOME /var/lib/gems
ENV GEM_PATH /var/lib/gems
ENV PATH $PATH:/var/lib/gems/bin

ADD common.sh \
    install-sdk.sh \
    /usr/local/lib/arvbox/

RUN mkdir -p /var/lib/arvados/git /var/lib/gems /var/lib/pip

ARG arvados_version

RUN cd /usr/src && \
    git clone https://github.com/curoverse/arvados.git 
    #git clone --no-checkout https://github.com/curoverse/arvados.git && \
    #git -C arvados checkout ${arvados_version}

RUN /usr/local/lib/arvbox/install-sdk.sh

RUN mkdir /data
WORKDIR /data
