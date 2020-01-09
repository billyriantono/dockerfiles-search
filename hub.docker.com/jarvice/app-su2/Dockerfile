FROM nimbix/ubuntu-base:trusty
MAINTAINER stephen.fox@nimbix.net

# https://github.com/su2code/SU2/wiki/Parallel-and-CGNS-build

ENV SU2_VERSION=4.3.0
ENV BUILD_DIR=/tmp/build
ENV HDF5_VER=1.8.17

# Install add-apt-repository
RUN apt-get update && apt-get install -y \
    software-properties-common \
    python-software-properties \
    git \
    python-pip \
    python-setuptools \
    python-virtualenv \
    python3-pip \
    python-matplotlib \
    python3-matplotlib \
    python3.4-venv \
    pkg-config

# Install system packages
RUN apt-get update && apt-get install -y python-pip \
    libblas-dev \
    python-dev \
    libpython-dev \
    python-dev \
    libpython3-dev \
    python3-dev \
    libopenblas-base \
    libopenblas-dev \
    liblapack3gf \
    liblapack-dev \
    build-essential \
    python-numpy \
    python-scipy \
    gfortran

RUN sudo pip install --upgrade numpy
RUN sudo pip install --upgrade scipy

# Install package dependencies (requires gcc-4.9 runtime)
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/ppa
RUN apt-get update && apt-get install --upgrade -y \
    swig \
    gcc-4.9 \
    gcc-4.9-base \
    libstdc++6

WORKDIR ${BUILD_DIR}
RUN apt-get update && apt-get install -y \
    curl \
    libibverbs-dev \
    libibverbs1 \
    librdmacm1 \
    librdmacm-dev \
    rdmacm-utils \
    libibmad-dev \
    libibmad5 \
    byacc \
    libmlx5-1 \
    libibumad-dev \
    libibumad3 \
    flex
RUN curl -O http://mvapich.cse.ohio-state.edu/download/mvapich/mv2/mvapich2-2.2.tar.gz
RUN tar xvf mvapich2-2.2.tar.gz

WORKDIR ${BUILD_DIR}/mvapich2-2.2
RUN ./configure RSH_CMD=/usr/bin/ssh SSH_CMD=/usr/bin/ssh
RUN make -j4
RUN make install

RUN mkdir -p "${BUILD_DIR}/hdf5"
WORKDIR "${BUILD_DIR}/hdf5"
RUN curl -o hdf5-${HDF5_VER}.tar.gz "https://www.hdfgroup.org/ftp/HDF5/current/src/hdf5-${HDF5_VER}.tar.gz" && tar xvf hdf5-${HDF5_VER}.tar.gz
WORKDIR "${BUILD_DIR}/hdf5/hdf5-${HDF5_VER}"
RUN CC=/usr/local/mvapich2/bin/mpicc ./configure --enable-parallel --prefix="/usr/local/hdf5-${HDF5_VER}" | tee -a hdf5-config.log && \
    make clean && \
    CC=/usr/local/mvapich2/bin/mpicc ./configure --enable-parallel --prefix="/usr/local/hdf5-${HDF5_VER}" | tee -a hdf5-config.log  && \
    make -j4 | tee -a make.log && \
    make install

RUN mkdir -p "${BUILD_DIR}/CGNS"
WORKDIR "${BUILD_DIR}/CGNS"
RUN wget "https://github.com/CGNS/CGNS/archive/v3.2.1.tar.gz"
RUN tar xvf v3.2.1.tar.gz
WORKDIR "${BUILD_DIR}/CGNS/CGNS-3.2.1"
RUN mkdir -p /usr/local/CGNS
RUN mkdir build
WORKDIR "${BUILD_DIR}/CGNS/CGNS-3.2.1/build"
RUN CMAKE_PREFIX_PATH="/usr/local/hdf5-${HDF5_VER}" \
    CMAKE_C_COMPILER=/usr/local/mvapich2/bin/mpicc \
    cmake \
    -DCGNS_ENABLE_64BIT=on \
    -DCGNS_ENABLE_TESTS=on \
    -DCGNS_BUILD_SHARED=on \
    -DCGNS_BUILD_CGNSTOOLS=on \
#    -DCGNS_ENABLE_HDF5=on \
#    -DHDF5_NEED_MPI=on \
#    -DHDF5_INCLUDE_DIRS="/usr/local/hdf5-${HDF5_VER}" \
#    -DHDF5_LIBRARIES="/usr/local/hdf5-${HDF5_VER}/lib" \
    -DCMAKE_INSTALL_PREFIX=/usr/local/CGNS-3.2.1 \
    .. && \
    make -j4 && \
    make install

RUN mkdir -p ${BUILD_DIR}/su2-build
WORKDIR ${BUILD_DIR}/su2-build

RUN git clone https://github.com/su2code/SU2.git
WORKDIR ${BUILD_DIR}/su2-build/SU2
RUN git checkout v${SU2_VERSION}
RUN ./configure \
    --enable-mpi \
    --with-cc=/usr/local/bin/mpicc \
    --with-cxx=/usr/local/bin/mpicxx \
    --with-CGNS-lib=/usr/local/CGNS-3.2.1/lib \
    --with-CGNS-include=/usr/local/CGNS-3.2.1/include \
    --enable-PY_WRAPPER \
    --prefix=/usr/local/su2/${SU2_VERSION} \
    CXXFLAGS="-O3"
RUN make -j4
RUN make install

# Cleanup temporary files
RUN rm -rf ${BUILD_DIR}
RUN apt-get clean && rm -rf /var/lib/apt/*

ADD ./scripts /usr/local/scripts
RUN chown -R 555 /usr/local/scripts

USER nimbix
