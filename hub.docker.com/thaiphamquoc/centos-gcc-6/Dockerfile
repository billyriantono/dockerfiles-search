FROM centos:7.3.1611
MAINTAINER tpham

USER root

ENV GCC_VERSION="6.3.0" \
    THREADS=4 \
    WORK_DIR=/tmp/gcc6

RUN yum install -y gcc gcc-c++ git cmake wget bzip2 make

WORKDIR ${WORK_DIR}
RUN wget https://ftp.gnu.org/gnu/gcc/gcc-${GCC_VERSION}/gcc-${GCC_VERSION}.tar.bz2 && tar xf gcc-${GCC_VERSION}.tar.bz2
RUN sed -i s/ftp:/https:/ gcc-${GCC_VERSION}/contrib/download_prerequisites

WORKDIR ${WORK_DIR}/gcc-${GCC_VERSION}
RUN ./contrib/download_prerequisites

RUN mkdir ${WORK_DIR}/gcc-build
WORKDIR ${WORK_DIR}/gcc-build
RUN ../gcc-${GCC_VERSION}/configure --prefix=/home/vagrant/install/gcc-${GCC_VERSION} --enable-languages=c,c++ --disable-multilib
RUN make -j $THREADS && make install

RUN ln -s /home/vagrant/install/gcc-${GCC_VERSION}/bin/gcc /usr/local/bin/gcc-6 && \
    ln -s /home/vagrant/install/gcc-${GCC_VERSION}/bin/g++ /usr/local/bin/g++-6 && \
    ln -s /home/vagrant/install/gcc-${GCC_VERSION}/bin/gcc /usr/local/bin/cc && \
    ln -s /home/vagrant/install/gcc-${GCC_VERSION}/bin/g++ /usr/local/bin/c++

ENV CC=gcc-6 \
    CXX=g++-6

WORKDIR /

RUN rm -rf /tmp/gcc6
