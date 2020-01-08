FROM debian:jessie
MAINTAINER Edward Fauchon-Jones <edward.fauchon-jones@ligo.org>

# use omen mirror for debian
RUN echo "# debian repos defined in /etc/apt/sources.list.d" > /etc/apt/sources.list
RUN echo "deb http://omen.phys.uwm.edu/debian jessie main" > /etc/apt/sources.list.d/debian.list
RUN echo "deb http://omen.phys.uwm.edu/debian jessie-updates main" > /etc/apt/sources.list.d/debian-updates.list
RUN echo "deb http://omen.phys.uwm.edu/security jessie/updates main" > /etc/apt/sources.list.d/debian-security.list

# install updates
RUN apt-get update
RUN apt-get -yqq upgrade

# install apt-utils, build-essential, git, and wget
RUN apt-get -yqq install apt-utils build-essential git wget

# add htcondor repository
RUN echo "deb http://omen.phys.uwm.edu/htcondor jessie stable" > /etc/apt/sources.list.d/htcondor.list
RUN wget -qO - http://omen.phys.uwm.edu/keys/nemo.key | apt-key add -

# add gridtools repository
RUN echo "deb http://omen.phys.uwm.edu/gridtools jessie main" > /etc/apt/sources.list.d/gridtools.list
RUN wget -qO - http://omen.phys.uwm.edu/keys/lscsoft-2016.key | apt-key add -

# add lscsoft repository
RUN echo "deb http://omen.phys.uwm.edu/lscsoft jessie contrib" > /etc/apt/sources.list.d/lscsoft.list
RUN wget -qO - http://omen.phys.uwm.edu/keys/lscsoft.key | apt-key add -

# update repository metadata
RUN apt-get update

# install required dependencies
RUN apt-get -yqq install autoconf
RUN apt-get -yqq install automake
RUN apt-get -yqq install bc
RUN apt-get -yqq install help2man
RUN apt-get -yqq install ldas-tools-framecpp-dev
RUN apt-get -yqq install libcfitsio-dev
RUN apt-get -yqq install libchealpix-dev
RUN apt-get -yqq install libfftw3-dev
RUN apt-get -yqq install libframe-dev
RUN apt-get -yqq install libglib2.0-dev
RUN apt-get -yqq install libgsl0-dev
RUN apt-get -yqq install libhdf5-dev
RUN apt-get -yqq install libmetaio-dev
RUN apt-get -yqq install liboctave-dev
RUN apt-get -yqq install libopenmpi-dev
RUN apt-get -yqq install libtool
RUN apt-get -yqq install libxml2-dev
RUN apt-get -yqq install pkg-config
RUN apt-get -yqq install python-dev
RUN apt-get -yqq install python-pip
RUN apt-get -yqq install python-glue
RUN apt-get -yqq install python-h5py
RUN apt-get -yqq install python-healpy
RUN apt-get -yqq install python-numpy
RUN apt-get -yqq install python-scipy
RUN apt-get -yqq install python-shapely
RUN apt-get -yqq install python-matplotlib
RUN apt-get -yqq install python-pytest
RUN apt-get -yqq install python-six
RUN apt-get -yqq install swig3.0

# Prepare environment for LALSuite
ENV LALSUITE_SRCDIR /src
ENV LALSUITE_PREFIX /opt/lalsuite
RUN mkdir -p ${LALSUITE_SRCDIR} \
 && mkdir -p ${LALSUITE_PREFIX}

# Download LALSuite
RUN cd ${LALSUITE_SRCDIR} \
 && git clone https://github.com/lscsoft/lalsuite.git

# Install LALSuite
RUN cd ${LALSUITE_SRCDIR}/lalsuite \
 && ./00boot \
 && ./configure \
    --prefix=${LALSUITE_PREFIX} \
    --enable-swig-python \
    --disable-lalstochastic \
    --disable-lalxml \
    --disable-lalinference \
    --disable-laldetchar \
    --disable-lalapps

RUN cd ${LALSUITE_SRCDIR}/lalsuite \
 && make \
 && make install
