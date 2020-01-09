FROM fedora:latest
MAINTAINER Krishna Kumar <kks32@cam.ac.uk>

# Update to latest packages, remove vim-minimal & Install Git, GCC, Clang, Autotools and VIM
RUN dnf update -y && \
    dnf remove -y vim-minimal python sqlite && \
    dnf install -y boost boost-devel clang cmake cppcheck dnf-plugins-core eigen3-devel findutils gcc gcc-c++ \
                   git hdf5 hdf5-devel kernel-devel lcov \
                   make openmpi openmpi-devel sqlite sqlite-devel tar tbb tbb-devel valgrind vim \
                   voro++ voro++-devel vtk vtk-devel wget && \
dnf clean all


# Install MKL
RUN dnf config-manager --add-repo https://yum.repos.intel.com/mkl/setup/intel-mkl.repo && \
    rpm --import https://yum.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB && \
    dnf install -y intel-mkl

RUN source /opt/intel/compilers_and_libraries/linux/bin/compilervars.sh -arch intel64 -platform linux


# Coverage 
# RUN wget http://ftp.de.debian.org/debian/pool/main/l/lcov/lcov_1.13.orig.tar.gz && tar xf lcov_1.13.orig.tar.gz && make -C lcov-1.13/ install

# Create a user cbcities
RUN useradd cbcities
USER cbcities

# Create a research directory and clone git repo of pipe-network code
RUN mkdir -p /home/cbcities/research && \
    cd /home/cbcities/research && \
    git clone https://github.com/cb-cities/pipe-network.git

# Done
WORKDIR /home/cbgeo/research/pipe-network

RUN source /opt/intel/compilers_and_libraries/linux/bin/compilervars.sh -arch intel64 -platform linux

RUN /bin/bash "$@"
