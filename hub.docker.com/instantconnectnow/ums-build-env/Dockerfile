FROM           centos:centos6.6
MAINTAINER     Matt DeFano

# Install basic stuff
RUN yum -y update &&\
    yum clean all

# Install EPEL repository
RUN yum -y install wget &&\
    yum clean all &&\
    wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm

# Install dev tools 
RUN yum -y --nogpgcheck install libmpc-devel mpfr-devel gmp-devel yum-plugin-ovl tar zlib-devel openssl-devel sqlite-devel makedepend which &&\
    yum -y groupinstall "Development Tools" &&\
    yum clean all

# Build GCC 4.9.3 (gcc/g++)
RUN curl ftp://ftp.mirrorservice.org/sites/sourceware.org/pub/gcc/releases/gcc-4.9.3/gcc-4.9.3.tar.bz2 -O &&\
    tar xfj gcc-4.9.3.tar.bz2 &&\
    cd gcc-4.9.3 &&\
    ./contrib/download_prerequisites &&\
    ./configure --disable-multilib --enable-languages=c,c++ &&\
    make -j `grep processor /proc/cpuinfo | wc -l` &&\ 
    make install &&\
    rm -rf /gcc-4.9.3*

# Install ISO-generation tools (from EPEL)
RUN rpm -ivh epel-release-latest-6.noarch.rpm &&\
    yum -y install xorriso &&\
    yum clean all

# Install CMake/CMake3
RUN yum -y install epel-release cmake3 &&\
    yum clean all &&\
    ln -s /usr/bin/cmake3 /usr/bin/cmake

# Build Python 2.7
RUN wget http://python.org/ftp/python/2.7.14/Python-2.7.14.tar.xz &&\
    tar xf Python-2.7.14.tar.xz &&\
    cd Python-2.7.14 &&\
    ./configure --prefix=/usr/local --enable-unicode=ucs4 --enable-shared LDFLAGS="-Wl,-rpath /usr/local/lib" &&\
    make &&\
    make altinstall &&\
    rm -f /Python-2.7.14.tar.xz &&\
    rm -rf /Python-2.7.14

# Install Pip and Conan
RUN curl https://bootstrap.pypa.io/get-pip.py | /usr/local/bin/python2.7 &&\
    pip install conan 

# Hack to accommodate Makefiles that have hard-coded path to GCC
RUN mkdir -p /opt/gcc-4.9.2 &&\
    ln -s /usr/local/bin /opt/gcc-4.9.2

# CMake-required environmental variables
ENV AR="/usr/bin/ar"
ENV CC="/usr/local/bin/gcc"
ENV CPP="/usr/local/bin/gcc -E"
ENV CXX="/usr/local/bin/g++"
ENV CXXCPP="/usr/local/bin/g++ -E"